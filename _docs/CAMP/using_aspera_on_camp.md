---
title: Using Aspera on CAMP
category: CAMP
order: 3
---

To use Aspera on CAMP:

1. Load an Aspera module. You can find versions of Aspera available on CAMP with `ml spider aspera`. 
As of 25/04/2021, only one version of Aspera (3.6.1) is available on CAMP. You can load it with `ml Aspera-Connect/3.6.1`.
2. In your `ascp` command, use `/camp/apps/eb/software/Aspera-Connect/3.6.1/etc/asperaweb_id_dsa.openssh` for `-i` option (setting the private SSH key to use).
3. Submit your `ascp` command to the queue for running on a computational node. You can edit the following example of an `sbatch` wrapper for your needs:
```
#!/usr/bin/env bash

#SBATCH --ntasks 1
#SBATCH --cpus-per-task 1
#SBATCH --mem 4G
#SBATCH --time 01:00:00

ml Aspera-Connect/3.6.1

# HG003
ascp -T \
-i /camp/apps/eb/software/Aspera-Connect/3.6.1/etc/asperaweb_id_dsa.openssh \
anonftp@ftp-trace.ncbi.nlm.nih.gov:ReferenceSamples/giab/data/AshkenazimTrio/HG003_NA24149_father/NIST_Illumina_2x250bps/reads/D2_S1_L001_R1_001.fastq.gz \
../data/fastq/hg003/D2_S1_L001_R1_001.fastq.gz
```
This script downloads a FASTQ file for a sample from the Genome In A Bottle (GIAB) project. By the way, for downloading data from GIAB, 
Aspera proved particularly useful, as `curl` or `lftp` were not able to download GIAB's `.gz` files properly (the files came with a broken format), 
and `ncftp` was paifully slow.

Please see [Aspera's command line docs](https://download.asperasoft.com/download/docs/ascp/3.5.2/html/dita/ascp_usage.html) for more info on options that you could use.
