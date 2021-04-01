---
title: Uploading data from CAMP to ArrayExpress
category: CAMP
order: 1
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
