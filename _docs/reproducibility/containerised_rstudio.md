---
title: Containerised RStudio on CAMP
category: Reproducibility
order: 6
---

Here are the steps required to run RStudio server in a Singularity container on CAMP:

1) Save the function below to your home directory (for example, into the `start_rstudio.sh` file):

```
#!/usr/bin/env bash

function singularity_rstudio() {
    while [[ $# -gt 0 ]]
    do
        case $1 in
        -v|--volume)
            local VOLUME="$2"
            ;;
        -c|--containder)
            local CONTAINER="$2"
            ;;
        esac
        shift
    done

    PORT=8787
    while true; do
        echo -n "Trying port $PORT ... "
        PORTPRESENCE=`ss -n | grep -w $PORT | wc -l`
        if [[ $PORTPRESENCE -eq 0 ]]; then
            echo "Success! The port is not in use."
            break
        fi
        echo "Port is in use."
        PORT=$((PORT+1))
    done

    link=http://$SLURMD_NODENAME.camp.thecrick.org:$PORT

    ml Singularity/2.6.0-foss-2016b
    export PASSWORD='password'
    export USERNAME=`id -un`

    echo "The RStudio-Server will be running on this address:"
    echo $link
    echo "Username:" $USERNAME
    echo "Password:" $PASSWORD

    singularity exec \
        -c \
        -B $VOLUME:/home/rstudio \
        $CONTAINER \
        rserver \
        --www-port $PORT \
        --www-address 0.0.0.0 \
        --auth-none=0 \
        --auth-pam-helper-path=pam-helper
}
```

2) If you are going to use the container with RStudio for the first time, pull a Docker image with the RStudio Server:

`singularity pull docker://rocker/rstudio:latest`

It will pull and build the image into the current directory. The building process may take several minutes. Move the container to another directory, if you like; it is especially useful to move it out of your home directory, if you have built it there, so it does not occupy very limited disk space. 

Next time you will skip this step.

3) Go to an interactive node. For example, the following command will give you an interactive node with 16 GB of memory for 16 hours:

`srun --ntasks=1 --mem=16G --time=16:00:00 --partition=int --pty bash`

It is useful to run this command from a `tmux` or `screen` session started on a login node, so you don't lose your interactive node with RStudio in case you disconnect from CAMP.

4) Upload ("source") this function into your Bash session: `source ~/start_rstudio.sh`.

5) Start RStudio by calling the function: 

`singularity_rstudio -v <volume_to_mount> -c <path_to_rstudio_container>`

A URL, username and password should now be displayed in the terminal. Use these to login to Rstudio server from your web browser.

6) Run `setwd('/home/rstudio')` in the RStudio console.

7) If you need an R package not installed in the RStudio container by default, then to get it in the container permanently you would need to put an installation command in the Dockerfile of the container and re-build it (still need to write this up), but you can also install R packages outside of the container while working in RStudio:

- On CAMP, inside the `volume_to_mount` directory, create a subdirectory `r_packages`.

- On CAMP, run exactly the same version of R you are running in RStudio (you can print the version of R with `R.version.string`). You can install the version of R you need from Bioconda or find it among Slurm modules available on CAMP with `ml spider R`.

- In the R console on CAMP, set the new installation location for packages: `.libPaths('<volume_to_mount>/r_packages')`.

- In the R console of RStudio, run the same command: `.libPaths('/home/rstudio/<path_to_r_packages_inside_volume_to_mount>/r_packages')` - so that RStudio knows where to look for packages.

- In the R console on CAMP, install the packages you need.

- Now, in the RStudio you should be able to access the installed packages with `library(<...>)`.

8) You need to provide the path to the installed packages every time you start the RStudio. So, in RStudio, after running `setwd('/home/rstudio')`, you will need to run `.libPaths('/home/rstudio/<path_to_r_packages_inside_volume_to_mount>/r_packages')` before running any other commands.

9) If you installed a package but it would not load because it needs one or more shared libraries that are missing in the container, you can solve the problem with the following steps:

- Find the necessary library (its name will be present in the error message) in your conda environment, if you have one (look into `<path/to/the/environment>/lib`). If you don't have a conda environment, you can create one using conda available among CAMP software modules (you can do `ml Anaconda3/2020.07` to load conda) and create an environment for libraries. Then install the library you need into this environment and find the installed library in the `lib` directory of the environment. In the error message from R, you will see the name of the soft link that should lead to the required library, so you can find the name of the soft link first and then see which file it directs to.

- In the volume that you have mounted to the RStudio container, create a directory for shared libraries (for example, `libs`).

- Copy the actual library file (not the soft link) from the environment into the `libs` directory and make a required soft link to it in that directory.

- In your R script, before the failing line that should load your package, add another line to load the shared library first: `dyn.load("<library_directory>/softlink")`. For example, if you copied a required library `libicudata.so.67.1` into a directory `libs` that you created in the mounted volume and made a soft link `libicudata.so.67` to the library, then the command would be `dyn.load("/home/rstudio/libs/libicudata.so.67")`. Your package may miss multiple shared libraries, and in that case you need to copy all of them into `libs` and add a `dyn.load(...)` command for each of them in your R script before loading the package. 
