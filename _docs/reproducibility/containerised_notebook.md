---
title: Containerised Jupyter notebook on CAMP
category: Reproducibility
order: 7
---

Here are the steps required to run Jupyter notebook server in a Singularity container on CAMP:

1) Save the function below to your home directory (for example, into your `~/.aliases.sh` file):

```
#!/usr/bin/env bash

function singularity_jupyter() {
        local PORT=8888
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

        ml Singularity/3.6.4

        mkdir -p ./notebook

        singularity exec \
            -c \
            --pwd /home \
            -B $VOLUME:/home \
            $CONTAINER \
            /opt/conda/envs/scvelo/bin/jupyter notebook \
            --no-browser \
            --port $PORT \
            --ip 0.0.0.0 \
            --notebook-dir=./notebook
}
```

2) If you are going to use the container with RStudio for the first time, pull a Docker image with Jupyter installed:

`singularity pull docker://<IMAGE>`

It will pull and build the image into the current directory. The building process may take several minutes. Move the container to another directory, if you like; it is especially useful to move it out of your home directory, if you have built it there, so it does not occupy very limited disk space. 

Next time you will skip this step.

3) Go to an interactive node. For example, the following command will give you an interactive node with 16 GB of memory for 16 hours:

`srun --ntasks=1 --mem=16G --time=16:00:00 --partition=int --pty bash`

It is useful to run this command from a `tmux` or `screen` session started on a login node, so you don't lose your interactive node with RStudio in case you disconnect from CAMP.

4) Upload ("source") this function into your Bash session: `source ~/.aliases.sh`.

5) Start Jupyter by calling the function: 

`singularity_jupyter -v <volume_to_mount> -c <path_to_singularity_container>`

By default the working directory will be mounted to the container if -v is not specified.

A URL should now be displayed in the terminal and is used to login to Jupyter from your web browser (i.e. http://int000:8888/?token=xxxxxxx). You will need to append '.camp.thecrick' to the URL for it to function correctly (i.e. http://int000.camp.thecrick:8888/?token=xxxxxxx).