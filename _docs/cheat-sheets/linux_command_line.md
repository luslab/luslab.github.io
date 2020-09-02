---
title: Linux command line
category: Cheat Sheets
order: 1
---

## Basic commands
- `cd <DIRECTORY>` - Change directory
- `cd ..` - Go up one directory
- `ls` - List. Lists all the files and folders contained in the current directory.
- `mv <filepathsource> <filepathtarget>` - Renames/moves a file from source to target
- `touch <newfile>` - Creates a new file without any content
- `cat <newfile>` - Creates a file with content
- `nano <file>` - Used to edit a text file


## Other commands
- `mkdir -p folder/subfolder` - Inculde creation of parent dir
- `tail -f` - Monitor a log file
- `ls -lah` - List files with detailed information
- `du -h -d1` - List top level directory space usage
- `srun --ntasks=1 --cpus-per-task=1 --partition=int --time=4:00:0 --mem=4G --pty /bin/bash` - Create interactive node on CAMP
- `pwd` - Show current path
- `whoami` - Current login username
- `tree` - Tree directory structure
- `ln -s <source> <dest>` - Symbolic link
- `find ./myfolder -mindepth 1 ! -regex '^./myfolder/test2\(/.*\)?' -delete` - this will delete all folders inside ./myfolder except that ./myfolder/test2 and all its contents will be preserved
