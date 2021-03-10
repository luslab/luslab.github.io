---
title: Calculate cluster space utilisation
category: How-to's
order: 3
---

This command will find all directories down to a specified level and pipe this to the `du` command before sorting. Using `xargs` enables the du command to use multiple cores.

```
find /camp/lab/luscomben/home/ -maxdepth 2 -type d | xargs -P 8 -I% sh -c 'du -hs %' | sort -hr
```

You can wrap also the overall command in an sbatch script and submit it to the slurm scheduler. Place the below example into a bash script e.g. `space_util.sh`. 

```
#!/bin/bash
#SBATCH --job-name=luslab_space_util
#SBATCH --mail-type=END,FAIL
#SBATCH --mail-user=chris.cheshire@crick.ac.uk
#SBATCH --output=luslab_space_util.out.txt
#SBATCH --error=luslab_space_util.err.txt
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --time=24:00:00
#SBATCH --mem=16G
#SBATCH --partition=cpu

## RUN SPACE UTIL
find /camp/lab/luscomben/home/ -maxdepth 2 -type d | xargs -P 8 -I% sh -c 'du -hs %' | sort -hr
```

To run this the script it must me given execution privilege.

```
chmod 755 space_util.sh
```

The script can now be submitted to the SLURM scheduler.

```
srun space_util.sh
```