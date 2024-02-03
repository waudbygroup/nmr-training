---
title: Linux Tutorial
layout: default
nav_order: 1
parent: Exercises
---

# Linux Tutorial for Beginners

## Introduction

Linux is a popular open-source operating system used on many scientific computers and servers. As an NMR spectroscopist, you'll likely need to interact with Linux systems to acquire and process your data. This tutorial provides a gentle introduction to the basic Linux skills you'll need.

## The Terminal

The terminal (also called the command line or shell) is a text-based interface allowing you to type commands to interact with the computer. It may look unfamiliar, but offers precise control.

## Directory Structure and Filenames

The Linux filesystem is a hierarchy of directories (folders). The root directory `/` contains subfolders like `/home` and `/usr`. Your home folder has a name like `/home/yourname`. File and folder names are case-sensitive.

## Navigating Directories

* To see your current directory, run `pwd` 
* To list folder contents, run `ls`. Use `ls -l` for more detail.
* To change directories, run `cd foldername`
* To go up a level, run `cd ..` 
* To return to home, `cd ~` or `cd` alone will work.

## Moving, Copying, Viewing & Editing

* To move/rename files, use `mv file1 file2`
* To copy files, use `cp file1 file2`

### Copying Recursively 

* `cp -r folder1 folder2` - copy folder1 contents to folder2 

## Viewing Files

There are several ways to view text files from the terminal:

* `less file1` - view contents page by page
* `more file1` - view contents one screen at a time  
* `cat file1` - print whole file contents at once
* `head file1` - show first 10 lines
* `tail file1` - show last 10 lines

Several utilities are also available to sort or search files:
* `sort file1` - sort contents alphabetically
* `grep "searchterm" file1` - search file for lines containing keyword

## Editing Text Files with Nano

Linux comes with a variety of editors that can be used to edit text files. Some of these are complex (but powerful), like `vi` or `emacs`. A simple editor to get started with is `nano`:
* `nano file1` - open nano editor
* Use arrow keys to move 
* Ctrl-X to exit, confirm save
* Ctrl-G show help menu

## Standard Input and Output

* Output goes to the terminal by default
* Use `> file1` to redirect output to a file instead
* Use `< file1` to redirect a command's input from a file

## Pipes

The `|` pipe redirects the output of one command as input to another. Very useful!

```
command1 | command2
```

## Compressing / Extracting Files

* `tar -czvf datafile.tgz datafile` - compress to datafile.tgz
* `tar -xzvf datafile.tgz` - extract datafile from datafile.tgz


## Connecting to Servers (ssh)  

Use `ssh` to securely log in to remote servers:

* `ssh username@hydrogen.nmrbox.org` - connect to NMRbox
* `exit` or Ctrl-D to logout


## Transferring Files (scp)

Use `scp` to securely copy files between systems. 

* `scp sourcefile user@helium.nmrbox.org:destination` - copy sourcefile to NMRbox
* `scp -r sourcefolder user@remotehost:destination` - recursive scp


## Test Yourself

1. Bruker title information for each experiment is stored in a file `title`, within the `pdata` and `1` folders. How would you view the contents of this file?
2. What command lists files in long format, including permissions and sizes?
3. How would you compress the contents of an experiment, and transfer it to nmrbox?
4. The `acqus` file within an experiment lists all the parameters used for its acquisition. How would you filter this file to find the `NS` parameter (the number of scans)?




