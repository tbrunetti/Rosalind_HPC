# Intro To Linux and the Rosalind HPC
--------------------------------------
The Linux and the command line may seem like a daunting undertaking initially, but with some practice and these basic commands, you should be able to navigate through Rosalind like a pro!  


**1.  Where Am I?! -- The 'pwd' command**
--------------------------------------
When you first log into Rosalind it will automatically place you in your home directory. The phrase yourUsername should be replaced with your Rosalind username. You can verify this by typing `pwd`, which stands for present working directory on the command prompt as follows:

```
[yourUsername@cubipmlgn01 ~]$ pwd
```
The output should look like this and then give you a new command prompt:
```
/homelink/yourUsername
[yourUsername@cubipmlgn01 ~]$
```


**2.  Changing Directories -- The 'cd' command**
-------------------------------------------------
Your home directory has very limited space and can only be viewed by you the user and nobody else. Therefore this space should never be used to upload data or for sharing files with other members within your project group.  Typically, this should only be used to store very small files that only you, the user, needs or for installing specific software or storing small reference files.  Instead, let's change directories into your shared project space on Rosalind.  The phrase "yourProject" should be replaced with the exact name of the project you are approved for on Rosalind and remember, Linux is **ALWAYS CASE SENSITIVE!**
```
[yourUsername@cubipmlgn01 ~]$ cd /gpfs/share/yourProject
```
To confirm this, you can use the `pwd` command from above to ensure you are now in your designated project space:
```
[yourUsername@cubipmlgn01 ~]$ pwd
/gpfs/share/yourProject
[yourUsername@cubipmlgn01 ~]$
```
The `cd` command can also regonize a very useful shortcut.  If you want to move up one directory/folder you can use `..`  For example if you type in the following:
```
[yourUsername@cubipmlgn01 ~]$ cd ..
```
you will now have moved up one level.  To confirm this, if you type in the pwd command, you should now see the following:
```
[yourUsername@cubipmlgn01 ~]$ pwd
/gpfs/share
[yourUsername@cubipmlgn01 ~]$
```
To change directories back into your project, you can type the following:
```
[yourUsername@cubipmlgn01 ~]$ cd yourProject
```


**3.  Make a new directory (folder) -- The 'mkdir' command**
------------------------------------------------------------
Now that you are in your project directory you have the ability to create new folders, or in Linux we all them directories. Let's make a new folder called `Rosalind_Demo`.
```
[yourUsername@cubipmlgn01 ~]$ mkdir Rosalind_Demo
[yourUsername@cubipmlgn01 ~]$
```
You have now successfully created a directory called `Rosalind_Demo`.  You may be wondering how you can tell...well let's move to the next step.  



**4.  List all items in a directory -- The 'ls' command**
----------------------------------------------------------
The `ls` command is one of your best friends when using the command line.  `ls` stands for list segments, and any time you call it, it will list all the items in your present working directory.  For example type the following:
```
[yourUsername@cubipmlgn01 ~]$ ls
```
It should return the following (assuming you followed the directions above):
```
Rosalind_Demo
[yourUsername@cubipmlgn01 ~]$
```
If you have other files or directories in this directory it will list those as well.  Additionally ls has multiple options you can add following the `ls` command.  One of which that is particular useful is `-lh`  This means long format and human readable.  For example, type in the following:
```
[yourUsername@cubipmlgn01 ~]$ ls -lh
```
You should see something similar to the following:
```
drwx------  2 yourUsername groupOwnership 4.0K Sep 28 14:13 Rosalind_Demo
```
`drwx------` tells you the directory or file permissions. The 4.0K tells you the size of the directory (note, this is a little confusing because directories are always 4.0K no matter what is in them) or file. The `h` in `-lh` makes it so that the size is human readable i.e. KB, MG, GB) istead of in bytes).  The date and time following the size is the date the file/directory was last modified.  The point being, the `-lh` flag can provide you with more detailed information about every item in your directory.  We will revisit the meaning of the `drwx------` in a bit.


**5.  How can other users within my group project access my directories and files?! -- 'The 'chmod' command**
--------------------------------------------------------------------------------------------------------------
The first letter, 'd', indicates that Rosalind_Demo is a directory.  The remaining letters specify which users and groups have access to the directory `Rosalind_Demo`.  Since you created this directory, by default you also own the directory, therefore, the 'rwx', following the 'd' indicates that you have the ability to read/open Rosalind_Demo (the r), you also have write/modify access (the w), and you have the ability to execute or move into the `Rosalind_Demo` directory (the x).  Please download the supplemental PDF, "Understanding_File_Permissions_in_Linux.pdf" located in the supplemental_PDFs files in this github directory.  Also located here: https://github.com/tbrunetti/Rosalind_HPC/blob/master/supplemental_PDFs/Understanding_File_Permissions_in_Linux.pdf


**6.  Moving and copying files -- The 'mv' and 'cp' commands**
---------------------------------------------------------------
Next, we are going to move files to other locations or make copies of them elsewhere.  You must be **very careful** with these commands because they will overwrite exisiting files if you decide to copy or move them to a place where a file with the same name exists. First, lets create a file in the `Rosalind_Demo` directory that was just created in the previous steps.  Make sure to change directories into `Rosalind_Demo`.  Next we are going to open a text editor in Rosalind.  Rosalind has emacs, nano, vi/vim installed.  For the purpose of this demo, I am going to use vim.
```
vim testing_Rosalind.sh
```
This will open a the vim text editor.  We can type in anything we want here from text to code. For an example, I am going to write a simple shell script that you can copy and paste into this window or type out the following:  (PRESS 'i' first, you should see that the mode in the bottom-left corner now has changed to **--INSERT--** mode which means you can type/copy/paste.
```vim
#!/bin/bash

echo 'Hello!  My name is Rosalind!'
```
To save this file and exit vim  press **ESC** followed by typing **:wq** and then press **ENTER**.  
When you list the files in `Rosalind_Demo` you should now see the file/shell script you just created called testing_Rosalind.sh.



## Helpful Hints for Beginning Linux
------------------------------------
Here are some helpful 'best practices' when using Linux.  It will save you some frustrations, until you feel more comforatable with the command line!
* DO NOT use any kind of whitespace (i.e. no spaces, no tabs, etc...) in the names of files or directories
* Double-tab following a command and path can give the user a list of all the possible autofill options
* Avoid using the `rm`, `rm -r` or `rmdir` unless you are ***100% sure you will never ever need those files and directories again.  Once they are deleted, they are gone forever!***

