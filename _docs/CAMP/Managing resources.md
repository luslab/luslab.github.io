---
title: Managing Resources
category: CAMP
order: 2
---

## Check how many CPUs the lab is using

As a lab and as individuals we have limits on the number of CPUs we can use at any one time. The up-to-date info for that is [here](https://wiki.thecrick.org/display/HPC/Running+jobs+on+CAMP).

To check the lab CPU usage use the following command:

`squeue --account u_luscomben --format "%u§%i§%.30j§%P§%C§%m§%M§%L§%t§%.15N§%.15R§%.19S§%20Y" | column --table --separator §`

To check the submission time, start time, time taken to run and memory usage of a job you can use saact, for example:

`sacct -o JobID,Submit,Start,Elapsed,TotalCPU,MaxRSS -j <jobID>`
