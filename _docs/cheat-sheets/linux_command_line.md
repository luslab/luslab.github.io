---
title: Linux command line
category: Cheat Sheets
order: 1
---

**Note:** Don't write Bash scripts, only one-liners! (Use Python for scripting.)

See the full Bash manual [here](https://www.gnu.org/software/bash/manual/bash.html).

## General
- `echo $?` - Print **exit status** of the last command: 0 if the last command exited successfully and a non-zero value otherwise 
- `command1 | command2` - Execute `command1` and redirect its `stdout` into `stdin` of `command2`
- `command1 && command2` - Execute `command1` and then execute `command2` only if `command1` exited successfully
- `command1; command2` - Execute `command1` and then `command2` independently of the success of `command1`
- `command > file` - Redirect `stdout` of `command` into `file`; the `file` gets overwritten
- `command >> file` - Add the output of `command` to the end of `file`
- `command 2> file` - Redirect `stderr` to `file`
- `command 2>&1` - Redirect `stderr` to `stdout`
- `command 2> /dev/null` - Remove `stderr`
- `<(command2)` - **Process substitution**: treat `stdout` of `command2` as a file. **Note:** There should be no space between `<` and `(`. 
- `diff <(ls dir1) <(ls dir2)` - Example of process substitution: find differences between lists of files in `dir1` and `dir2` (`diff` needs two files as arguments)
- `command1 | tee file | command2` - `tee` splits `stdout` of `command1` and writes one copy into `file` while feeding the other copy into `stdin` of `command2`
- `(command1; command2; ...; commandN)` - **Command grouping**: `stdout` streams of `command1`, `command2`, ..., `commandN` are collected and can be redirected together
- `(echo -n "a"; echo "b") > f.txt` - Example of command grouping: print `ab` into `f.txt`.
- `PATH=PATH:/path/to/add` - Add `/path/to/add` to the value of the `PATH` variable
- `whoami` - Print your current username

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
