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
drwx------  2 yourUsername yourUsername 4.0K Sep 28 14:13 Rosalind_Demo
```
`drwx------` tells you the directory or file permissions. The 4.0K tells you the size of the directory (note, this is a little confusing because directories are always 4.0K no matter what is in them) or file. The `h` in `-lh` makes it so that the size is human readable i.e. KB, MG, GB) istead of in bytes).  The date and time following the size is the date the file/directory was last modified.  The point being, the `-lh` flag can provide you with more detailed information about every item in your directory.  We will revisit the meaning of the `drwx------` in a bit.


**5.  How can other users within my group project access my directories and files?! -- 'The 'chmod' command**
--------------------------------------------------------------------------------------------------------------
Linux allows users to control what users and groups can have access to partiular directories and files, assuming as user has access to your project.  There are 3 types of permissions/access that you should be aware of:  read, write, and execute.  Please download the supplemental PDF, "Understanding_File_Permissions_in_Linux.pdf" located in the supplemental_PDFs files in this github directory.  Also located here: https://github.com/tbrunetti/Rosalind_HPC/blob/master/supplemental_PDFs/Understanding_File_Permissions_in_Linux.pdf  This should give you an understanding of what the permissions mean and why it is important to understand how these work.  Make sure you are located in your project directory and then type in the following:
```
[yourUsername@cubipmlgn01 ~]$ ls -lh
```
You should see something similar to the following:
```
drwx------ 2 yourUsername yourUsername 4.0k Sep 28 14:13 Rosalind_Demo
[yourUsername@cubipmlgn01 ~]$ 
```
All of your pemission can be read by looking only at `drwx------`.  From reading the PDF mentioned above you should have a basic understanding of what the letters and dashes mean.  The first letter, 'd', indicates that `Rosalind_Demo` is a directory.  The remaining letters specify which users and groups have access to the directory `Rosalind_Demo`.  Since you created this directory, by default you also own the directory, therefore, the 'rwx', following the 'd' indicates that you have the ability to read/open `Rosalind_Demo` (the r), you also have write/modify access (the w), and you have the ability to execute or move into the `Rosalind_Demo` directory (the x).  Let's say a member of your group project wants to read a file or go into your directory, but you do not want them to be able to modify file or directories.  You can give only members in your group only read and executable access.  First you should change your group ownership to whatever your group name is on Rosalind.  For example if my group name on Rosalind is "myGroupName" then you can change the group ownership by typing in the following command:
```
[yourUsername@cubipmlgn01 ~]$ chown :myGroupName Rosalind_Demo
[yourUsername@cubipmlgn01 ~]$
```
Now if you list what is in your current project directory you will notice that the directory Rosalind_Demo is now owned by the myGroupName group:
```
[yourUsername@cubipmlgn01 ~]$ ls -lh
drwx------ 2 yourUsername myGroupName 4.0k Sep 28 14:17 Rosalind_Demo
```
Notice how the only thing that changed is who or what set of users owns the group.  Now you can change group permissions (if you read the PDF you will now this is the second set of dashed triplets in the permissions column).  Changing permissions is performed using the `chmod` command:
```
[yourUsername@cubipmlgn01 ~]$ chmod g+rx Rosalind_Demo
[yourUsername@cubipmlgn01 ~]$
```
In the command above, the g indicates you want to modify **g**roup permission by adding, denoted by the **+** symbol, read and executable permissions, as denoted by **rx**.  You can check that this was changed by again using `ls -lh`.
```
[yourUsername@cubipmlgn01 ~]$ ls -lh
drwxr-x--- 2 yourUsername myGroupName 4.0k Sep 28 14:30 Rosalind_Demo
```
Let's say you made a mistake and you did not want to give the group read permissions.  You can easily take away these permissions by using the minus **-** symbol:
```
[yourUsername@cubipmlgn01 ~]$ chmod g-r Rosalind_Demo
[yourUsername@cubipmlgn01 ~]$ ls -l
drwx--x--- 2 yourUsername myGroupName 4.0k Sep 28 14:31 Rosalind_Demo
```
Below is a cheat sheet of some of the more common combinations used on Rosalind you can give `chmod` and what permissions are being granted.  It is worth noting that once you give a permssion in order to take it away you must use the minus (-) sign followed by the permission you want to remove for that file/directory.  

|COMBO|MEANING|
|---|---|
|u+x | give the owner (yourself) permission to execute a file|
|u+rwx | give the owener (yourself or person who created it) permission to read, write, and execute a file|
|u+rw | give the owner (yourself or perons who created it) permission to only read and write a file|
|g+r | give group read only permissions|
|g+w | give a group write only permissions|
|g+x | give group executable only permissions (needed to get into a directory)|
|g+rwx | give a group read, write, and executable permissions|
g-w | remove write permissions to the group
g-x | remove executable permission to the group



**6.  Copying and moving files -- The 'cp' and 'mv' commands**
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
When you list the files in `Rosalind_Demo` you should now see the file/shell script you just created called testing_Rosalind.sh. Since this is a script, we should change the permissions to be executable:
```
[yourUsername@cubipmlgn01 ~]$ chmod u+x testing_Rosalind.sh
[yourUsername@cubipmlgn01 ~]$ 
```
Let's say now we decide we need another script that is the same as the one we just wrote but we want to add another line.  We can copy this scrpt to another file using the `cp` command.  The first sting following `cp` is the name of the file you want to copy while the string following that is the new name of the copied file:
```
[yourUsername@cubipmlgn01 ~]$ cp testing_Rosalind.sh new_Rosalind_test_file.sh
```
The first string following `cp` is the name of the file you want to copy while the string following that is the new name of the copied file.  Now if you list your files you will see both your original and your copy:

```
[yourUsername@cubipmlgn01 ~]$ ls -lh
-rwx------ 1 yourUsername myGroupName 49 Sep 28 15:01 new_Rosalind_test_file.sh
-rwx------ 1 yourUsername myGroupName 49 Sep 28 15:00 testing_Rosalind.sh
```
You will also notice when you copy a file, the permissions of the original file are adopted by the newly copied file.

How about we decide we want to make a new directory to keep all of our scripts organized.  First we have to make that directory:
```
[yourUsername@cubipmlgn01 ~]$ mkdir scripts
[yourUsername@cubipmlgn01 ~]$ ls -lh
-rwx------ 1 yourUsername myGroupName 49 Sep 28 15:01 new_Rosalind_test_file.sh
drwx--S--- 2 yourUsername myGroupName 4.0K Sep 28 15:12 scripts
-rwx------ 1 yourUsername myGroupName 49 Sep 28 15:00 testing_Rosalind.sh
```
You can see that by listing everything in the `Rosalind_Demo` directory you can see your newly created <span style="color:blue">`scripts`</span> directory.  Now we can move all of your scripts inside the scripts directory by using the `mv` command:
```
[yourUsername@cubipmlgn01 ~]$ mv new_Rosalind_test_file.sh scripts
```
Where the name of the file you want to move is the first string following the 'mv' command.  The next string is the name of the file/directory destination you want to move the file to.
```
[yourUsername@cubipmlgn01 ~]$ ls -lh
drwx--S--- 2 yourUsername myGroupName 4.0K Sep 28 15:12 scripts
-rwx------ 1 yourUsername myGroupName 49 Sep 28 15:00 testing_Rosalind.sh
[yourUsername@cubipmlgn01 ~]$ cd scripts
[yourUsername@cubipmlgn01 ~]$ ls -lh
-rwx------ 1 yourUsername myGroupName 49 Sep 28 15:01 new_Rosalind_test_file.sh
```
You can see that you have now successfully moved `new_Rosalind_test_file.sh` into the scripts directory.  Now let's move up one directory back to the `Rosalind_Demo` directory.
```
[yourUsername@cubipmlgn01 ~]$ cd ..
```
Let's say you want to change the name/rename the `testing_Rosalind.sh` script.  You can also use the `mv` command here.  **Be very careful here.  If you rename the file to name that already exists in the directory, it will overwrite it!!!**
```
[yourUsername@cubipmlgn01 ~]$ mv testing_Rosalind.sh renamed_testing_Rosalind.sh
[yourUsername@cubipmlgn01 ~]$ ls -lh
-rwx------ 1 yourUsername myGroupName 49 Sep 28 15:52 renamed_testing_Rosalind.sh
drwx--S--- 2 yourUsername myGroupName 4.0K Sep 28 15:12 scripts
```
You can see that the original script we created `testing_Rosalind.sh` has now updated its file name to `renamed_testing_Rosalind.sh`.



## Helpful Hints for Beginning Linux
------------------------------------
Here are some helpful 'best practices' when using Linux.  It will save you some frustrations, until you feel more comforatable with the command line!
* DO NOT use any kind of whitespace (i.e. no spaces, no tabs, etc...) in the names of files or directories
* Double-tab following a command and path can give the user a list of all the possible autofill options
* Avoid using the `rm`, `rm -r` or `rmdir` unless you are ***100% sure you will never ever need those files and directories again.  Once they are deleted, they are gone forever!***

