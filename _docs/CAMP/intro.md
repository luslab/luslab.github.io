---
title: Intro
category: CAMP
order: 1
---

## Introduction to CAMP

CAMP is our high performance cluster at the Crick.
People have different attitudes, some run most of their analysis on personal laptop and use the cluster when necessary.
Others run most of their analysis on CAMP regardless.

- I'm stuck! - Post on [#hpc](https://app.slack.com/client/T0H1NAC7M/C2Z0C6Y1L/details/top) channel on Crick Computing Chat Slack workspace, you will often get a fast reply. People also post here if they think the cluster is running slowly or broken.

- I'm stuck but I'm embarassed - Sometimes we post on [#lus-hpc](https://app.slack.com/client/T0H1NAC7M/G4HDXGVC3/details/top) to ask questions just to other people in the lab if we feel like they might know or answer quicker.


### Getting access

There are two main parts to CAMP, CAMP compute and CAMP storage, and you will need access to both.
Access to CAMP storage lets you mount CAMP folders onto your laptop and read/write files.
Access to CAMP compute lets you access the cluster via ssh and send jobs .etc.

To request access email the IT helpdesk - its-helpdesk@crick.ac.uk, you will need to generate a public key to send to the HPC team. 

Here are some instructions on how to do this:

Open a terminal window. At the shell prompt, type the following command:

`ssh-keygen -t rsa`

The ssh-keygen program will prompt you for the location of the key file. Press Return to accept the defaults. You can optionally specify a passphrase to protect your key material. Press Return to omit the passphrase. The output of the program will look similar to this:

```
Enter file in which to save the key (/Users/tony/.ssh/id_rsa):
Created directory '/Users/tony/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/tony/.ssh/id_rsa.
Your public key has been saved in /Users/tony/.ssh/id_rsa.pub.
```

### Once you have an account, how to log on

You can log on to CAMP via ssh, we have access to two login nodes - login000 and login001. If there is a problem with one, you might try the other:

`ssh -XY login000.camp.thecrick.org`

Once you logon you'll find yourself in a directory with very little space, where you will not want to save anything.
Most people will symbolically link their working directory to this directory so they can easily go there when they log on.

### Directory structure on CAMP

The base directory is /camp/. From there you will mostly be using /camp/lab/luscomben/home/. Other labs have their own folders in the "lab" directory. If you find yourself working with another lab a lot, you might consider asking for a project directory between the two labs, this should simplify sharing because both labs should then have access to the directory. e.g we have a shared directory with the Jernej Ule lab at /camp/project/proj-luscombe-ule.

From /camp/lab/luscomben/home/ there are two main directories: shared and users. Everyone has their own personal folder on users and this what I mean when I refer to the "working directory". The shared folder contains data that we all have access to and so we like to keep this tidy. We ask that whenever someone finds themselves downloading a resource file, such as a genome, an annotation .etc that they try and add this to the shared folder so that we can save duplicating large files in our personal directories.

The structure of the shared folder is:

```
/camp/lab/luscomben/home/shared
├── archive
|   └── folder structures that have been archived, so we can easily see in case we want to get things back
├── legacy
|   └── murky secrets from the lab's dark past, best left alone
├── projects
|   └── if you have within lab projects you might consider making a shared directory here, for multi-lab projects best to ask for a project folder
├── ref
    └── genomes
        └── human
        └── mouse
        └── yeast
        └── etc
```
