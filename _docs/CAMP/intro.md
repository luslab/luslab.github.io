---
title: Intro
category: CAMP
order: 4
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

