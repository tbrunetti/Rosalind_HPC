# Intro To Linux and the Rosalind HPC
--------------------------------------
The Linux and the command line may seem like a daunting undertaking initially, but with some practice and these basic commands, you should be able to navigate through Rosalind like a pro!  


**1.  Where Am I?! -- The 'pwd' command**
--------------------------------------
When you first log into Rosalind it will automatically place you in your home directory. The phrase yourUsername should be replaced with your Rosalind username. You can verify this by typing 'pwd', which stands for present working directory on the command prompt as follows:

```
[yourUsername@cubipmlgn01 ~]$ pwd
```
The output should look like this and then give you a new command prompt:
```
/homelink/yourUsername
[yourUsername@cubipmlgn01 ~]$
```


**2.  Changing Directories -- The 'cd' command**
-----------------------------------------------
Your home directory has very limited space and can only be viewed by you the user and nobody else. Therefore this space should never be used to upload data or for sharing files with other members within your project group.  Typically, this should only be used to store very small files that only you the user needs or for installing specific software or storing small reference files.  Instead, let's change directories into your shared project space on Rosalind.  The phrase "yourProject" should be replaced with the exact name of the project you are approved for on Rosalind and remember, Linux is **ALWAYS CASE SENSITIVE!**
```
[yourUsername@cubipmlgn01 ~]$ cd /gpfs/share/yourProject
```
To confirm this, you can use the pwd command from above to ensure you are now in your designated project space:
```
[yourUsername@cubipmlgn01 ~]$ pwd
/gpfs/share/yourProject
[yourUsername@cubipmlgn01 ~]$
````
