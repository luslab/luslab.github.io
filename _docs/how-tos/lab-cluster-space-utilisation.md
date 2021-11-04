---
title: Calculate cluster space utilisation
category: How-to's
order: 3
---

This command will find all directories down to a specified level and pipe this to the `du` command before sorting; using `xargs` enables the `du` command to use multiple cores:

```
find /camp/lab/luscomben/home/ -maxdepth 2 -type d | xargs -P 8 -I% sh -c 'du -hs %' | sort -hr
```

A convenient way of running this command is to wrap it in an `sbatch` script and submit it to the slurm scheduler. 

To do that, place the code below into a bash script e.g. `space_util.sh`: 

```
#!/bin/bash
#SBATCH --job-name=luslab_space_util
#SBATCH --mail-type=END,FAIL
#SBATCH --mail-user=<your.name>@crick.ac.uk
#SBATCH --output=luslab_space_util.out.txt
#SBATCH --error=luslab_space_util.err.txt
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --time=8:00:00
#SBATCH --mem=4G
#SBATCH --partition=cpu

## RUN SPACE UTIL
find /camp/lab/luscomben/home/ -maxdepth 2 -type d | xargs -P 8 -I% sh -c 'du -hs %' | sort -hr
```

and put your email address instead of `<your.name>@crick.ac.uk` if you would like to receive an email when the script fails or finishes successfully. If you don't want to receive an email from SLURM, please remove the instruction `#SBATCH --mail-user=<your.name>@crick.ac.uk`.

Give the script execution privileges

```
chmod 755 space_util.sh
```

and submit it to the SLURM scheduler

```
sbatch space_util.sh
```

Any errors will be logged in `luslab_space_util.err.txt`, and if the script finished successfully, it will output the list of users, sorted by the disk space that they currently occupy, into `luslab_space_util.out.txt`.
