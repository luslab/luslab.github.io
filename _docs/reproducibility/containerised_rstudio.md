---
title: Containerised RStudio on CAMP
category: Reproducibility
order: 6
---

Here are the steps required to run RStudio server in a Singularity container on CAMP:

1) Save the function below to your home directory (for example, into the `~/.aliases.sh` file):

```
#!/usr/bin/env bash

function singularity_rstudio() {
        local PORT=8787
        local VOLUME=$(pwd)
        while [[ $# -gt 0 ]]
        do
            case $1 in
            -v|--volume)
                local VOLUME=$2
                ;;
            -c|--container)
                local CONTAINER=$2
                ;;
                -p|--port)
                local PORT=$2
                ;;
            esac
            shift
        done


        if [ -z ${CONTAINER+x} ]; then
                RED='\033[0;31m'
                NC='\033[0m' # No Color
                printf "${RED}ERROR:${NC} --container not set!\n"
                return
        fi

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

        ml Singularity/3.6.4
        export PASSWORD='password'
        export USERNAME=`id -un`
        export R_USER=$USER && [ "$(id -u)" == "1000" ] && export R_USER=rstudio

        echo "The RStudio-Server will be running on this address:"
        echo $link
        echo "Username:" $USERNAME
        echo "Password:" $PASSWORD
        echo "Volume mounted:" $VOLUME

        # Make tmp directories in home in order to be able to install packages within the container
        mkdir -p $HOME/.rstudio-server/run
        mkdir -p $HOME/.rstudio-server/tmp

        singularity exec \
        -c \
        --pwd /home/$R_USER \
        -H $VOLUME:/home/$R_USER \
        -B $HOME/.rstudio-server:/var/lib/rstudio-server \
        -B $HOME/.rstudio-server/run:/run \
        -B $HOME/.rstudio-server/tmp:/tmp \
        -B $VOLUME:/home/$R_USER \
        $CONTAINER rserver \
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

4) Upload ("source") this function into your Bash session: `source ~/.aliases.sh`.

5) Start RStudio by calling the function: 

`singularity_rstudio -v <volume_to_mount> -c <path_to_rstudio_container>`

By default the working directory will be mounted to the container if `-v` is not specified.

A URL, username and password should now be displayed in the terminal. Use these to login to Rstudio server from your web browser.

7) If you need an R package not installed in the RStudio container by default, then to get it in the container permanently you would need to put an installation command in the Dockerfile of the container and re-build it. However you can install packages within the container using `install.packages()`. These will be stored in `$HOME/.rstudio-server` and will be available when restarting the container.
