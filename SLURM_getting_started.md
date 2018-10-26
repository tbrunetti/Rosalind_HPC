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

Be aware, that there are some libraries that exist that have multiple versions available.  It is good practice to always `purge` your environment each time you compile new software and re-load the modules you would like after loading `slurm`.  For example, there may be some libraries in R that require v3.4 but will not work on v3.3.  If a user already has a R module pre-loaded, it may default to a version of R they may not want and therefore, the program will fail because of incorrect versioning within their environment.  Please `purge` and `load` to prevent such errors!
```
module purge
module load slurm
module load <my module>
```


<div class="paragraph"><p><br>
<br></p></div>  

## Submitting A Batch Script

In order for SLURM to submit and schedule your job for processing, it requires special formatting of some headers in your shell script to indicate how the job should be processed. For more information please [click here](https://github.com/tbrunetti/Rosalind_HPC/blob/master/rosalind-getting-started.md#running-jobs)

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

__Interactive Sessions for Users who are Members of Multiple Groups__  
If a user is a member of multiple groups on Rosalind, srun must also be run with the `--account` argument so it is clear which speedtype needs to be charged for time consumed.  If this argument is left off, the `srun` command will fail and the user not be able to run an interactive session. Here is an example of how to request an interactive session if the user is part of more than one group:
```
srun --account myGroupName-$USER --time=60 -p defq -n1 --pty  python
```
The `$USER` field can remain exactly as is (literally $USER), but change the myGroupName to whichever group that the time should be charged.  The `--account myGroupName-$USER` must directly follow the `srun` command.
<div class="paragraph"><p><br>
<br></p></div>  

## Check Job Status, Job Stats, and overall Queue

After a user submits batch job to SLURM, a user may want to know what the status is of their job (PENDING, RUNNING, COMPLETED).  SLURM supports the `sacct` command to look at only the users' list of submitted jobs for the day.
```
sacct
       JobID    JobName  Partition    Account  AllocCPUS      State ExitCode 
------------ ---------- ---------- ---------- ---------- ---------- -------- 
136761            MyJob     matlab ticr-user+          1    RUNNING      0:0
136762           MyJob2       defq ticr-user+          1  COMPLETED      0:0 
136762.batch      batch            ticr-user+          1  COMPLETED      0:0 
```
The `JobID` is important for canceling or checking the status of a submitted job that has not yet been completed.  The `JobName` will match what the user has submitted in the header section of the batch script, while `Parition` specifies which queue the job was submitted.  If a queue is not specified within the batch script, the job is automatically sent to `defq`.  `Account` lets the user know which group/speedtype the charges are being billed.  `AllocCPUS` shows the user how many CPUs were requested for the job.  Similar information can be found by also using the `squeue -u <your_username>`.  This will show the user jobs that are PENDING in the queue or are RUNNING in the queue but not jobs that have been completed.  

To check the status overall queue in Rosalind you can use the `squeue` command.  This will give you all the the jobs on Rosalind that are either RUNNING or PENDING depending on resource availability.
```
squeue
JOBID 	PARTITION     NAME       USER 	ST           TIME  NODES NODELIST(REASON)  
136763	     defq  funProj    smithab  RUNNING	  10:12:01      1 cubipmcmp001		
136764	     defq  newProj    smithab  RUNNING	  12:24:52      5 cubipmcmp001 
136765	   bigmem  largePr    johnsxz  RUNNING	 1-4:18:38      1 cubipmbigmem01
136766	   bigmem  largePr    johnsxz  RUNNING	 1-5:32:27      1 cubipmbigmem02
136766	   bigmem  largePr    johnsxz  PENDING	 	        1 (RESOURCES)
```

Finally, a user may be interested in the statistics of a particular job that is running.  The `sstat <your_JobID>` command can be used to give the user an idea of the resources being used on a __running__ job. This only works for jobs submitted using the `srun` command.  To check the stats of a __currently running__ job submitted using `sbatch` use the following command `sstat <your_JobID>.batch`.  The `.batch` extension is critical for all jobs submitted as a batch script. For some general statistics on a job that has __already been completed__ one can use the following command:
```
sacct -j <your_jobid> --format=JobID,JobName,MaxRSS,Elapsed
```

<div class="paragraph"><p><br>
<br></p></div>  

## Cancelling Submitted Jobs

There are instaces when a user may want to cancel a submitted job currently PENDING or RUNNING in the job queue.  This can be done with the `scancel <your_JobID>` command.  If a user would like to cancel __all__ jobs they have submitted to the queue, the `-u` argument can be added like so:
```
scancel -u <your_username>
```
Additionally, a user can choose to cancel a job by the name they specified in the batch script. For example:
```
scancel --name <your_JobName>
```
It should be noted, that job cancellation can only be executed by the user who has submitted the job.


<div class="paragraph"><p><br>
<br></p></div>  

## Submitting Collections/Array of Jobs



<div class="paragraph"><p><br>
<br></p></div>  

## Estimating HPC Usage (Rosalind-Specific command)
A user may be interested in how many compute hours they have used during the current billing cycle (from the 1st-30/31st).  This can be estimated by calling `estimate-usage` on the command-prompt.  It will list the estimated number of compute hours used by that user.  If a user belongs to more than one group on Rosalind, it will list the number of compute hours billed to each group by that user.
