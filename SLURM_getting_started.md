# Basic SLURM Commands



## List and Load Available Modules
There are some libraries and programs already pre-installed globally on Rosalind.  Within the context of the SLURM framework, these are called modules.  Modules can be loaded in your environment or loaded within a batch script so you can freely use it without having to manually install and compile these program/libraries within your local HPC environment.  To view all available modules on Rosalind, you can type the following on the command prompt:  
```
module avail
```
To see what modules you currently have loaded into your personal environment, you can type the following:
```
module list
```
To load a module you can use module load like so:
```
module load python
```
This will load the Python programming language into your environment.  The `load` command can be followed by any of the available module names listed using `module avail`.

<div class="paragraph"><p><br>
<br></p></div>  

## Submitting A Batch Script

In order for SLURM to submit and schedule your job for processing, it requires special formatting of some headers in your shell script to indicate how the job should be processed.

<div class="paragraph"><p><br>
<br></p></div>  

## Running Interactive Jobs

There may be instances where a user chooses to run a program interactively.  This is analagous to opening a command prompt specific to a programming language the user would like to utilize, except in this case, the user can harness the power of Rosalind on the backend.  In these cases, the `srun` command can be used.  For lanuages such as Python and R, where they are available as modules and are open-source the following command can be used:
```
srun --time=60 -p defq -n1 --pty R
```
You can replace R with Python if you need an interactive Python session.  The above command will get you an interactive session for 60 minutes (--time=60) on a default/standard compute node (-p defq) using only one node (-n1).  You can change these parameters to fit your needs.  For queue options (-p) please visit the [Nodes and Queues wiki here](https://github.com/tbrunetti/Rosalind_HPC/blob/master/Nodes_and_Queues.md)

__Interactive Sessions on a Python Virutal Environment__
For those users who would like to run an interactive Python sesion within your virtual environment please be sure to:
1.  Activate the virtual environment
2.  Add `-E` as an argument to your `srun` call as follows:
```
srun -E --time=60 -p defq -n1 --pty  python
```
This will ensure that all of your libraries available in your virtual environment get carried over into the interactive session.  

__Interactive Sessions for MATLAB and SAS__
Since MATLAB and SAS are not open-source, it requires that certain nodes on Rosalind have a valid paid license in order to use the software. Due to this requirement, you must first use the `srun` command to request an available SAS or MATLAB node. For example, to run SAS you would run the following:
```
srun --time=60 -p sas -n1 --pty bash -l   
```
And then you must call the executable program on the command prompt to initiate the session:
```
/opt/SAS/9.4/SASFoundation/9.4/bin/sas_en -nodmsexp
```
Now you are running an interactive SAS session.  Keep in mind, when you are finished, you must exit twice for MATLAB and SAS interactive sessions.  For more information and detailed instructions about running SAS and MATLAB interactively please visit the [Nodes and Queues wiki here](https://github.com/tbrunetti/Rosalind_HPC/blob/master/Nodes_and_Queues.md) 

__Interactive Sessions for Users who are Members of Muliple Groups__
If a user is a member of multiple groups on Rosalind, srun must also be run with the `--account` argument so it is clear which speedtype needs to be charged for time consumed.  If this argument is left off, the `srun` command will fail and the user not be able to run an interactive session. Here is an example of how to request an interactive session if the user is part of more than one group:
```
srun --account myGroupName-$USER --time=60 -p defq -n1 --pty  python
```
The `$USER` field can remain exactly as is (literally $USER), but change the myGroupName to whichever group that the time should be charged.  The `--account myGroupName-$USER` must directly follow the `srun` command.
<div class="paragraph"><p><br>
<br></p></div>  

## Check Job Status and Queue



<div class="paragraph"><p><br>
<br></p></div>  

## Cancelling Submitted Jobs



<div class="paragraph"><p><br>
<br></p></div>  

## Submitting Collections/Array of Jobs



<div class="paragraph"><p><br>
<br></p></div>  

## Estimating HPC Usage (Rosalind-Specific command)
