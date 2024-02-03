---
title: Linux Tutorial
layout: default
nav_order: 1
parent: Exercises
---

# Linux Tutorial for Beginners

## Introduction

UNIX and Linux are operating systems used for lots of scientific computing, including NMR acquisition, processing and data analysis, and molecular dynamics. Mac OS is also built on top of UNIX and a terminal is built into the system. As an NMR spectroscopist, you'll likely need to interact with Linux systems to acquire and process your data. This tutorial provides a gentle introduction to the basic Linux skills you'll need.

Working with UNIX systems can be a bit intimidating, because they're usually accessed through a text interface (the 'command line', also called the terminal or shell). It may look unfamiliar, but offers precise control. After a while though you'll realise that it's not so difficult, and in fact can make a lot of repetitive tasks much easier!


## Directory Structure and Filenames

Unix uses a hierarchical file system structure, much like an upside-down tree, with a root directory `/` at the base of the file system that contains subfolders like `/home` and `/usr`. Directories and files are separated using a forward slash `/`.

![Illlustration of a typical UNIX filesystem][1]

The home directory contains directories for each user, in which their documents and data are stored (on a mac, the home directory is called `Users`).  Your home folder has a name like `/home/yourname`. Your home directory is also represented by the shortcut character `~`.

When you're working in the terminal, it's important to be aware of what directory you're currently working in - this is called the *working directory* and is often displayed as part of the terminal prompt.

There are a few special directory names it's useful to be aware of:

* Tilde `~` is shorthand for your home directory
* A period `.` refers to the current directory - this might not seem very useful at first, but there's a couple of important uses for it:
  * If you want to move something into the current directory, you can move it into `.`
  * To run a script in the current directory, you usually need to run it with `./myscript` - i.e. explicitly telling the computer to look for the script in the current directory.
* Two periods `..` refers to the parent directory. Similarly, `../..` refers to the direct two levels up, etc.

Some things to be aware of:

* Filenames and commands in unix are case sensitive – e.g. `MyFile` is different from `myfile`
* Avoid special characters and spaces in filenames. Underscores `_` and dashes `-` are good to use.
* Spaces and other special characters can be handled by 'escaping' them, which means putting a backslash before them. For example, a folder 'My NMR experiments' would be accessed as `My\ NMR\ experiments`.
* Files and folders that begin with a dot `.` are hidden. This is often used for settings and preferences to stop them cluttering up your directories.

## Your first commands

* `echo "Hello world"` prints 'Hello world' to the display
* `history` displays a list of previous commands

## Navigating Directories

* To see your current directory, run `pwd` 
* To list folder contents, run `ls`. Use `ls -l` for more detail.
  * `ls dirname` shows the contents of the named directory
* To change directories, run `cd foldername`
* To go up a level, run `cd ..` 
* To return to home, `cd ~` or `cd` alone will work.

Use tab completion to quickly navigate paths - type a few letters and press tab.

## Moving, Copying and Deleting Files

* To move/rename files, use `mv file1 file2`
  * `mv mydir/myfile .` - move a file 'myfile' in directory 'mydir' into the current directory
  * `mv oldname newname` - rename a file (literally, moving it from the old name to the new name)
* To copy files, use `cp file1 file2`
* To make a new directory, using `mkdir directoryname`
* To delete (remove) files, using `rm file`

{: .warning}
> In Linux, deleting files and folders is irreversible - there is no recycle bin or trash can. Be very careful, particularly when using the `rm -r` command.

### Copying and deleting recursively 

By default, commands only work on a single file. To copy or remove an entire folder, you need to include the `-r` *switch* after the command name:

* `cp -r folder1 folder2` - copy folder1 contents to folder2 
* `rm -r folder1` - delete folder1 and all its contents


## Viewing Files

There are several ways to view text files from the terminal:

* `less file1` - view contents page by page. Use up and down arrows to scroll, space to jump pages, and `q` to quit
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

## Compressing / Extracting Files

* `tar -czvf datafile.tgz datafile` - compress to datafile.tgz
* `tar -xzvf datafile.tgz` - extract datafile from datafile.tgz

## Escape keys:

* `Control+C` is a pretty universal 'cancel' instruction to stop a script that's running
* `Control+D` means 'end of input' and is often used to quit programs like python or Julia.
* `Control+Z` tells the process currently running to go to sleep. You can bring it back to the foreground again using the command `fg`, or send it to run in the background using `bg`.


## Wildcards

Wildcards are special characters used to refer to lots of files together:
* `*` refers to any number of characters
  * `rm data*` would delete all files beginning with 'data'
  * `cp rawdata/*.txt results/` would copy all files inside the folder 'rawdata' that end in '.txt' into the 'results' directory
  * You can use multiple wildcards at once, e.g. `rm */pdata/*/1r` would delete files called 'XXX/pdata/YYY/1r' 
* `?` refers to a single character
  * `rm 1?` would delete files '1r', '1i', but not '1rr'
  * `rm 2??` would delete files `2rr` but not `2r` or `2rrr`
* `*` and `?` can be combined, e.g. `*/pdata/*/2??`


## Connecting to Servers (ssh)  

Use `ssh` to securely log in to remote servers:

* `ssh username@hydrogen.nmrbox.org` - connect to NMRbox
* `exit` or Ctrl-D to logout


## Copying data to/from servers (scp)

Data is transferred to/from remote servers using `scp` (secure copy). It uses a similar syntax to `cp`, but (a) you need to provide additional information about the remote server, and (b) you can't use wildcards.

Remote addresses are specified as `user@server:path/filename`.

Examples:
* `scp -r myexpt cwaudby@argon.nmrbox.org:~/Documents/` copy recursively the folder 'myexpt' and its contents from the current (local) directory to the server 'argon.nmrbox.org', user 'cwaudby', and put it in the directory `~/Documents/` on the server (i.e. in the Documents folder within the home directory).
* `scp -r cwaudby@argon.nmrbox.org:~/Documents/myexpt .` copy the folder 'myexpt' on the remote server to the current (local) directory


## File permissions and the PATH

All files on UNIX systems have *permissions* associated with them, which determines whether you're allowed to read (r) from them, write (w) to them, or execute (x) them as a program. You can grant different levels of access to yourself (the user, 'u'), to a group of users (g) or to all users (a). You'll usually only be concerned about access for your own account (u-level access).

You can see what permissions a file has using the `ls -l` command, e.g.:

```
(base) ➜  ~ ls -l
total 41688
-rw-r--r--    1 chris  staff   628902 23 Sep  2021 1ak4.cif
```

The string `-rw-r--r--` on the left indicates the permissions. In order, these ten symbols indicate:
* `d` if it's a directory
* `rwx` permissions for the user
* `rwx` permissions for the group
* `rwx` permissions for all users

You can change permissions using the `chmod` command, e.g.:
* `chmod u+x file1` adds e(x)ecutable permission to the file for your (u)ser only
* `chmod u-x file1` removes e(x)ecutable permission to the file for your (u)ser only
* `chmod u+w file1` adds (w)rite permission to the file for your (u)ser only
* `chmod a+r file1` adds (r)ead permission for (a)ll users

The most common reasons to change permissions are to make new scripts executable, or to correct permissions for files that have been transferred to/from a remote server.

### The PATH

When you want to run a command, the system needs to know where to find the program file. This might seem obvious if it's in the current directory, but the computer assumes nothing!

You can provide the path to the file directly when you run the script, e.g. `./nmrproc.com` will run the `nmrproc.com` script located in the current directory `.`.

Alternatively, the terminal has a list of locations it knows to search when a command is entered - this is called the PATH. You can see it's contents by running `echo $PATH` (the dollar sign tells the shell to return the contents of the variable that follows it):

```
(base) ➜  ~ echo $PATH
/Users/chris/.gem/ruby/2.6.0/bin:/Users/chris/git/pp/util:/Users/chris/opt/miniconda3/bin:/Users/chris/opt/miniconda3/condabin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/TeX/texbin:/opt/X11/bin:/Applications/Visual Studio Code.app/Contents/Resources/app/bin:/Users/chris/Downloads/release-UnidecNMR-main/bin:/Users/chris/.npm-packages/bin
```

When installing a new program, be aware you might need to add it to the path!

## Standard input, output and pipes

Unix processes can take input, and produce output and/or error messages. The input channel is referred to as *standard input* or `stdin`, and the output channel is *standard output* or `stdout`. The error channel is `stderr`, but we won't worry about it too much here.

![Illustration of stdin, stdout and stderr][2]

Normally, `stdout` is displayed on the screen as the program runs. However, it's possible to divert the output to a file using the `>` operator, e.g.:
```
ls -l > myoutputfile.txt
```
will create a file, `myoutputfile.txt`, containing the results of the command `ls -l`. If the file doesn't already exist it will be created, and if it does exist it will be *overwritten*.

You can *append* output to an existing file using the `>>` operator, e.g.:
```
echo "Here is a status update" >> logfile
```

You can also send the contents of a file to standard input using the `<` operator, e.g.:
```
cat < myfile
```
would display the contents of the file 'myfile'. This isn't usually so useful because you could run the command more simply as `cat myfile` instead.

The real power of these ideas comes through the *pipe* operator `|` (above the backslash key on mac keyboards). This lets you connect the output of one command to the input of one command to the input of another.

![Illustration of piping commands][3]

As an example, you could pipe a directory listing to a `sort` command to produce sorted output:

```
(base) ➜  ~ ls | sort   
1ak4.cif
1eln.cif
1ezx.pdb
...
```

You can save the output of piped commands to files as well, e.g. `ls | sort > mysortedoutputfile`.

This approach is used extensively in NMR processing by nmrPipe, which pipes together NMR data between a series of processing commands, e.g.:
```
nmrPipe -in test.fid \
| nmrPipe  -fn SP -off 0.5 -end 1.00 -pow 2 -c 0.5    \
| nmrPipe  -fn ZF -auto                               \
| nmrPipe  -fn FT -auto                               \
...
```
Note that a backslash `\` at the end of a line indicates that the next line should be parsed as part of the same instruction. *Be aware - a common error in scripts is that line continuation backslashes might have an invisible space after them!*

## Scripting

Unix systems provide lots of handy little tools that you can use to make your life easier, particularly when piping them together into more complex scripts!

* `seq` produces a list of numbers
  * `seq 10` will output a list of numbers 1 to 10
  * `seq 10 20` will output a list of numbers from 10 to 20
  * `seq 10 20 100` will output numbers from 10 to 100 in steps of 20, i.e. 10, 30, 50, 70, 90.
* `grep` filters its input for a pattern
  * `cat myfile | grep NMR` would output all lines in 'myfile' containing 'NMR'
  * `cat myfile | grep -v NMR` would list all lines that *do not* contain NMR
* `sort` sorts the input into alphabetical order
  * `seq 10 | sort` would give the output 1, 10, 2, ... because 10 comes before 2 in alphabetical (dictionary) order
  * `sort -n` sorts in numerical order
  * watch out for any initial spaces in files - they'll be counted when sorting
* `sed` does find and replace, according to the instructions you provide it within single quotes
  * `sed 's/old/new/'` would substitute the first occurrence of 'old' with 'new'
  * `sed 's/old/new/g'` would replace *all* occurrences of 'old' with 'new' (the 'g' means global)
  * `sed 's/crystallography//g'` would delete all mentions of crystallography by replacing them with an empty string
* `awk` is a super useful program for working with tables of data - it can combine a series of filters `(...)` and commands `{...}` to manipulate data easily.
  * `awk '{print $1, $4}'` will print out the first and fourth columns of text in a file (separated by spaces and/or tabs)
  * `awk '(NR>3)'` prints all lines after the third line
  * `awk '($2>1000){print $2, $3}'` prints the second and third columns only if the second column is greater than 1000
  * `awk 'BEGIN{x=0} (NR>1){x=x+$3} END{print x}'` prints out the total of the third column, after ignoring the first line
  * look up some online tutorials for more examples - it's a powerful tool!


## Shells

The command line interface you see when you open up a terminal is called a *shell*. Confusingly, there's lots of different shells, which all work slightly differently when you start dealing with more advanced features:

* `bash` is the most common shell on linux systems
* `zsh` is the default shell on macs
* `csh` is an antique shell but it's heavily used by NMR packages like nmrPipe, so you'll probably need to use it a lot!

Shells are just programs, so you can open a different one just by entering it as a command - and you can quit using `exit`.


## Test Yourself

1. Bruker title information for each experiment is stored in a file `title`, within the `pdata` and `1` folders. How would you view the contents of this file?
2. What command lists files in long format, including permissions and sizes?
3. How would you compress the contents of an experiment, and transfer it to nmrbox?
4. The `acqus` file within an experiment lists all the parameters used for its acquisition. How would you filter this file to find the `NS` parameter (the number of scans)?




[1]: https://homepages.uc.edu/~thomam/Intro_Unix_Text/Images/unix_file_system.png
[2]: https://i.stack.imgur.com/LBRdx.png
[3]: https://docs.ycrc.yale.edu/PIL/fig/redirects-and-pipes.png
