---
title: Linux command line
category: Cheat Sheets
order: 1
---

Note: Don't write Bash scripts, only one-liners! (Use Python for scripting.)

## General
- command combination with ";", "|" and "&&"
- return code 
- redirection in general (> and >>)
- redirecting stdout and stderr (possibly, to /dev/null)
- process substitution
- command grouping
- xargs
- `whoami` - Current login username
- setting up PATH

## Operations with directories and files
- `pwd` - Show current path
- `cd <DIRECTORY>` - Change directory
- `cd ..` - Go up one directory
- rm
- `ls` - List. Lists all the files and folders contained in the current directory.
- `mv <filepathsource> <filepathtarget>` - Renames/moves a file from source to target
- `touch <newfile>` - Creates a new file without any content
- `cat > <newfile>` - Creates a file with content
- `nano <file>` - Used to edit a text file
- `mkdir -p folder/subfolder` - Inculde creation of parent dir
- `ls -lah` - List files with detailed information
- `du -h -d1` - List top level directory space usage
- `tree` - Tree directory structure
- `ln -s <source> <dest>` - Symbolic link
- `find ./myfolder -mindepth 1 ! -regex '^./myfolder/test2\(/.*\)?' -delete` - this will delete all folders inside ./myfolder except that ./myfolder/test2 and all its contents will be preserved
- stat
- cp
- vim

## Viewing and comparing files
- `tail -f` - Monitor a log file
- head
- less
- more
- wc
- grep
- diff
- comm

## Editing and summarising files
- awk (Note: AWK a language, not just a command, but please don't write scripts in AWK, only short one-liners)
- sed (Note: sed a language, not just a command, but please don't write scripts in sed, only short one-liners)
- tr
- sort
- uniq
- cut
- paste
- shuffle

## Other commands
- `srun --ntasks=1 --cpus-per-task=1 --partition=int --time=4:00:0 --mem=4G --pty /bin/bash` - Create interactive node on CAMP
