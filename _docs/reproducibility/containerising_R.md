---
title: Containerising R
category: Reproducibility
order: 5
---

<h1 id="run-rscript-on-camp-in-batch-mode">Run Rscript on CAMP in batch mode</h1>

You may find yourself wanting to run R scripts interactively in Rstudio whilst also maintaining reproducibility across both local and HPC systems. To do this you will need to build a Docker image containing R, Rstudio, and your required R packages. Luckily, the [rocker team](https://www.rocker-project.org/) have made base Docker images with R and Rstudio installed.

Here is an example Dockerfile which starts from the rocker/tidyverse Docker image.
```
FROM rocker/tidyverse:3.6.3

LABEL authors="alex.thiery@crick.ac.uk" \
      description="Docker image containing all requirements to run 10x analysis"

ARG WHEN

# Install apt packages
RUN apt-get update \
 && apt-get install -y --no-install-recommends \
 git=1:2.20.1-2+deb10u3 \
 apt-utils=1.8.2 \
 unzip=6.0-23+deb10u1 \
 procps=2:3.3.15-2 \
 build-essential=12.6 \
 zlib1g-dev=1:1.2.11.dfsg-1 \
 libxt-dev \
 libmagick++-dev \
 python-pip

RUN pip install pandas

RUN R -e "devtools::install_version('Seurat', version = '3.1.5', dependencies= NA)"
RUN R -e "devtools::install_version('future', version = '1.17.0', dependencies= T)"
RUN R -e "devtools::install_version('cowplot', version = '1.0.0', dependencies= T)"
RUN R -e "devtools::install_version('clustree', version = '0.4.2', dependencies= NA)"
RUN R -e "devtools::install_version('gridExtra', version = '2.3', dependencies=T)"
RUN R -e "devtools::install_version('getopt', version = '1.20.3', dependencies=T)"
RUN R -e "devtools::install_version('pheatmap', version = '1.0.12', dependencies=T)"
RUN R -e "BiocManager::install('limma')"
```

Next, you will need to build the image from the Dockerfile (this can also be done through github actions to save on computing power)
```
docker build -t <IMAGE>:<TAG> <FOLDER CONTAINING DOCKERFILE>
```

### Running Rstudio locally from within a container

In order to run Rstudio from within a container, you will first need to pull the image from DockerHub
```
docker pull <IMAGE>:<TAG>
```

Now that you have the image downloaded locally, you can load Rstudio to port 8787 and then access through the browser. The `-v` flag specifies the volume which you would like to mount to container - you will then have read/write access to this directory from within Rstudio.
```
docker run --rm -e PASSWORD=test -p 8787:8787 -v <DIR_TO_MOUNT>:/home/rstudio <IMAGE>:<TAG>
```

### Running R scripts within a container on CAMP

For some tasks, you may want to run R scripts on CAMP whilst using the same container but through the same container you have used locally. CAMP uses Singularity instead of Docker, however Singularity is capable of converting Docker images which is super handy.

First, start an interactive session on CAMP.
```
srun --ntasks=1 --cpus-per-task=2 --partition=int --time=1:00:0 --mem=16G --pty bash
```

Next, you will need to make a directory to store singularity images, as otherwise they will clogg up your home directory which has limited space.
```
mkdir ~/working/singularity
```

Symlink your singularity dir so that Singularity is able to access the downloaded images.
```
ln -s ~/working/singularity ~/.singularity
```

Now load singularity
```
ml Singularity
```

Download the Docker image of interest and convert to singularity
```
singularity pull --name ~/.singularity/<IMAGE_NAME> docker://<IMAGE>:<TAG>
```

From here, you can execute a shell script within the container
```
singularity exec ~/.singularity/<IMAGE_NAME> /bin/sh <PATH_TO_SHELL_SCRIPT>
```

Or you can load a shell session within the container and execute your scripts from within
```
singularity shell ~/.singularity/<IMAGE_NAME>
```


