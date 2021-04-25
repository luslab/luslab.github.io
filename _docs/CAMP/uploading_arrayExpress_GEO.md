---
title: Uploading data from CAMP to ArrayExpress and GEO
category: CAMP
order: 2
---

## Uploading data from CAMP to ArrayExpress

Uploading data to ArrayExpress directly from CAMP requires a few steps.

1. Module load ncftp `ml ncftp`
2. Change your ncftp configuration (located at ~/.ncftp/firewall) to be:
```
# NcFTP firewall preferences
# ==========================
firewall-type=8
firewall-host=10.28.7.200
firewall-port=21
firewall-exception-list=.camp.thecrick.org,.thecrick.org,.thecrick.test,localhost,localdomain
passive=on
```
3. You can now access ArrayExpress server and navigate to the specified folder in your submission:
`ncftp -u aexpress -p aexpress1 ftp-private-2.ebi.ac.uk`

## Uploading data from CAMP to GEO 

1. Create your personalised upload space at https://www.ncbi.nlm.nih.gov/geo/info/submissionftp.html
You will then be allocated a personalised directory for your GEO workspace e.g. `uploads/ojziff_MLcHSUY2`

2. Create a folder on CAMP containing all files for GEO upload:
- fastq files - ensure these are compressed
- processed data (e.g. differential gene expression results csv file)
- metadata csv file

Then check folder size `du -hs geo_submission_oct20/`  # 159G

3. Transfer files to your personalised upload space according to FTP upload instructions
Two options for transfer are with ncftpput or ncftp:

a) ‘ncftpput’ (transfers from the command-line without entering an interactive shell)
```bash
ml ncftp
sbatch -N 1 -c 8 --mem=0 -t 48:00:00 --wrap=“ncftpput -F -R -z -u  geoftp  -p “rebUzyi1"  ftp-private.ncbi.nlm.nih.gov  ./uploads/ojziff_MLcHSUY2  /camp/home/ziffo/home/projects/astrocyte-meta-analysis/reads/geo_submission_oct20" --job-name=ncftpput
```
b) ‘ncftp’ requires an interactive shell
```bash
ml ncftp
ncftp
set passive on
set so-bufsize 33554432
open  ftp://geoftp:rebUzyi1@ftp-private.ncbi.nlm.nih.gov
cd uploads/ojziff_MLcHSUY2
put -R /camp/home/ziffo/home/projects/astrocyte-meta-analysis/reads/geo_submission_oct20
```

4. After the FTP transfer is complete, notify GEO using the [Submit to GEO](https://submit.ncbi.nlm.nih.gov/geo/submission/)  web form

NB if you fail to notify them then the files will be automatically deleted from the server after two weeks. Once notified, they move the files to a safe location for review.
