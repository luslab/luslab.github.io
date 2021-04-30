---
title: Intro
category: Nextflow
order: 1
---

**Nextflow** is a language for pipeline development that became a standard in our lab.

We use Nextflow for:

 - Developing pipelines to process a particular type (or types) of data (for example, various CLIP datasets).
 - Make our computational projects reproducible.

If you need a pipeline to process a particular type of data, please check [our nf-core wiki page](../nf-core) first. 

If there is no pipeline for your data in the nf-core collection, or you are setting up your own project (and hence need to organise your data processing in a reproducible way), then you will need to write some Nextflow code! 

**Please make sure you use the DSL2 syntax when coding in Nextflow!**

DSL2 was released in July 2020 and will be the default format for all NF pipelines. DSL2 is a major revision of the Nextflow DSL that offers increased modularisation and scalability. 

#### DSL2 resources:
* [Introduction to DSL2](https://www.nextflow.io/blog/2020/dsl2-is-here.html)
* [Introduction to DSL2 in Nextflow](https://www.youtube.com/watch?v=I-hunuzsh6A)
* [Bytesize 5: DSL2 module development](https://nf-co.re/events/2021/bytesize-5-dsl2-module-development)
* [Nextflow DSL2 documentation](https://www.nextflow.io/docs/latest/dsl2.html)


#### Other resources on Nextflow - note these are not DSL2 specific:
* [Bytesize 1: Introduction to nf-core](https://nf-co.re/events/2021/bytesize-1-nf-core-into)
* [Full Nextflow course from Seqera Labs](https://seqera.io/training/)
* [Nextflow overall documentation](https://www.nextflow.io/docs/latest/index.html)
* [Nextflow coding patterns](https://nextflow-io.github.io/patterns/index.html)
* [Nextflow blog](https://www.nextflow.io/blog.html)
* [Nextflow resources](https://nf-co.re/usage/nextflow) (links to the same resources as above, but also to Nextflow tutorials and instructions on how to run Nextflow in the cloud)
* Also see [a very useful blog post](https://www.nextflow.io/blog/2019/easy-provenance-report.html) on how to track the provenance of results from a Nextflow pipeline.
 
#### You can get help regarding Nextflow here:

 1. `nextflow` Slack channel in our Crick workspace.
 2. [Nextflow mailing list](https://groups.google.com/forum/#!forum/nextflow)
 3. [Nextflow Gitter chat](https://gitter.im/nextflow-io/nextflow)
 4. [Nextflow on Slack](https://nf-co.re/join/) - useful channels include 'bytesize' (short weekly videos explaining different nextflow concepts), the 'help' channel and pipeline-specific channels


Also check out the other pages on our wiki, like [how to run Nextflow on CAMP](../../CAMP/running_nextflow).