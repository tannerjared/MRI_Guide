How to Process MRI Images:

1. [Beginner's Guide to Command-Line Interface](primer)
2. [Install Programs](Home)
3. Preprocessing T1 images
     * [Convert DICOM to NIfTI](dcm2nii)
     * [Align anterior commissure and posterior commisure](acpcdetect)
     * [Correct intensity nonuniformities (bias field)](N4BiasFieldCorrection)

---------------------------------------

Table of Contents:

[TOC]

---------------------------------------

[The full guide can be found here.](http://lifehacker.com/5633909/who-needs-a-mouse-learn-to-use-the-command-line-for-almost-anything)

# What is the command line?

The command-line interface, sometimes referred to as the CLI, is a tool into which you can type text commands to perform specific tasks as opposed to using the mouse to point and click on menus and buttons. Since you can directly control the computer by typing, many tasks can be performed more quickly, and some tasks can be automated with special commands that loop through and perform the same action on many files—saving you, potentially, loads of time in the process.

The application or user interface that accepts your typed responses and displays the data on the screen is called a shell, and there are many different varieties that you can choose from, but the most common these days is the Bash shell, which is the default on Linux and Mac systems in the Terminal application. By default, Windows systems only include the anemic Command Prompt application, which has nowhere near the power of Bash. You can use the open source Cygwin tool as your Windows command line if needed.

# Basic commands

To get started with the command line, you'll need to open up a terminal window and get ready to start typing commands. Here's a list of basic commands you can use, organized by the type of activity that you might want to perform.

When you run your terminal application (Cygwin on Windows, Terminal on Mac and Linux), your command prompt will start up pointing to a specific folder on your hard drive. You can navigate between folders, act on files inside those folders, or perform other actions.

## List files

First, let's display a list of files inside the active folder. For this task, you'll need to use the `ls` command. You can pass a number of parameters to the command to display extra details or change the sorting. For instance, if I add `-l` to the end of my ls command, I'll see a detailed listing; `-t` will sort the results by file time; `-S` will sort by file size; and `-r` will reverse the sorting. You could use a combination of these together, like this command, which will show all files sorted by file size with the largest files at the bottom:

```
#!console
$ ls -lSr
```

If you use the `–a` option, you can see hidden files, and you'll also notice something else in the listing: there are two entries for "." and ".." at the beginning of the list. These represent the current folder—the "." folder—and the parent folder—the ".." folder.

## Change directories

You can change between directories using the `cd` command, and using what we just learned about the ".." folder, you can use the following command to switch to the directory directly above the current one:

```
#!console
$ cd ..
```
You can navigate to either full or relative paths. For example, the command above navigates to a relative path—one above the current folder. If you're in /path/to/ and you want to navigate to the folder stuff inside that folder, you can simply type:

```
#!console
$ cd stuff
```

You can also navigate to absolute paths. Again, if I were in /path/to/ and I want to navigate to /another/path/, I would simply type:

```
#!console
$ cd /another/path
```
To swap directories to the previous working directory, the '-' (hyphen) shortcut is handy to have on hand. For example, if you were in the /first/folder/path/ directory and then switched over to /etc/ to make a configuration change, you might not want to type in the full path to switch back. You can quickly switch back to the previous working directory with this command:

```
#!console
$ cd -
```
