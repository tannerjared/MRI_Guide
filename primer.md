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

## Creating or removing folders

To create a new folder, you can simply use the `mkdir <foldername>` command. You can then remove any folder with the `rmdir <foldername>` command—as long as the folder is empty. If there are files in the folder, you'll have to delete those files before you can remove the folder.

## Creating and removing files

You can use the `touch <filename>` command to create a new, blank file, and then use the `rm <filename>` command to delete files:

```
#!console
$ rm filename
```

You can quickly remove all files in a directory by using the '*' (asterisk) wildcard—another simple tool that will come in very handy during your time in the command line. For example, if you're in a folder and want to delete every file inside that folder, just type:

```
#!console
$ rm *
```

If you want to delete a list of files and folders, including all files from subdirectories, without prompting you for every single entry, you can use the -r option for recursive, and the -f option for force. This command will wipe out every instance of a matching filename pattern (note the slightly different use of the wildcard) from the current directory and below:

```
#!console
$ rm -rf filename.*
```

# Beyond the basics

The following commands will be extremely useful to know when trying to run a whole set of participants at once. These commands go beyond the basic command lines.

## Running a script in the current folder

If you have an application or shell script in the current folder, you can't simply type the name of the command and expect it to start. You'll need to add a ./ to the beginning of the command in order to start it. Why? Because in the Bash shell, the current directory, or "." folder, is not included in the system path. So to launch scriptname.sh in the current folder, you'll need to use:

```
#!console
$ ./scriptname.sh
```

## Find files

You can use the very powerful `find` command to search for files on your system. For instance, if you wanted to find all files with .txt in the name that were modified in the last 5 days, you would use this command:

```
#!console
$ find . -name "*.txt" -mtime 5
```

The `grep` command can be used to quickly find text within files, even searching through subdirectories. For instance, if you wanted to search through all files in the current directory and below it for "text string", you could use this command:

```
#!console
grep -ir "text string" *
```

## Looping over a set of files

If you want to loop through a set of filenames and perform an action on each one, you can use the `for` command to loop through a set of files. For instance, to loop through all the .txt files in the current directory and display them on the console, you could use:

```
#!console
$ for f in *.txt
> do
> echo $f
> done
```

You can also combine the find command and the loop action to find specific files and then perform an action:

```
#!console
$ for i in $(find . -name "*.txt" -mtime 5)
> do
> echo $i
> done
```

# Using history

You can use the `history` command to show a list of all the recently used commands, or the up/down arrows to loop through them. The **Ctrl+R** shortcut key will start a search mode where you can type the first few characters of a command to search through your recent history.

# Using bash shortcut keys

There are a number of very useful shortcut keys you can use in the bash shell, and it pays to master them all. Here's a couple to get you started:

* Tab: Auto-complete files and folder names
* Ctrl + A: Go to the beginning of the line you are currently typing on
* Ctrl + E: Go to the end of the line you are currently typing on
* Ctrl + L: Clears the Screen, similar to the clear command
* Ctrl + U: Clears the line before the cursor position. If you are at the end of the line, clears the entire line.
* Ctrl + H: Same as backspace
* Ctrl + R: Let’s you search through previously used commands
* Ctrl + C: Kill whatever you are running
* Ctrl + D: Exit the current shell
* Ctrl + Z: Puts whatever you are running into a suspended background process. fg restores it.
* Ctrl + W: Delete the word before the cursor
* Ctrl + K: Clear the line after the cursor
* Ctrl + T: Swap the last two characters before the cursor
* Esc + T: Swap the last two words before the cursor
* Alt + F: Move cursor forward one word on the current line
* Alt + B: Move cursor backward one word on the current line
