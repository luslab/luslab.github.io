---
title: How to run Nextflow on CAMP?
category: CAMP
order: 3
---

You need CAMP to run Nextflow pipelines. 

In order to use Nextflow, on CAMP you need to load Nextflow as a pre-installed module, for example: `ml Nextflow/20.07.1`. 

**Make sure that you use the lastest version of Nextflow!** You can do it by first checking which versions of Nextflow are pre-installed on CAMP as modules (`ml spider Nextflow`) and then choosing the latest one.

Add the following:
- run nextflow with Crick config
- run an nf-core pipeline on CAMP (show a standard bash wrapper and comment on it)
