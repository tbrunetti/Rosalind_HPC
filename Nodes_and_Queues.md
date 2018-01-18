# Nodes and Queues Available
Rosalind has a few nodes and queues for which a user can choose to submit a job.  This becomes particularly important if a user requires any of the following specifications:
  * SAS
  * MATLAB
  * large memory requirements > 100GB
  * long run times > 36 hours  

This is because SAS and MATLAB are only currently available on a subset of standard compute nodes, and the default standard compute nodes only have a total of 128 GB of usable RAM. Although a user may specify a submitted batch job to run past 36 hours, SLURM automatically kills any jobs on the standard compute nodes surpassing this time limit unless a specific queue (longrun) is specified, regardless of the time specified by the user.

<div class="paragraph"><p><br>
<br></p></div>

## Compute Nodes
By default, if a user does not specify a node type, all jobs are submitted to one or more of the standard compute nodes.  In order to access a high memory node, a user must specify this in the SLURM script.  

Rosalind has two types of compute nodes available for general use:
  *  32 standard compute nodes
  *  2 high memory compute nodes

**The 32 standard compute nodes each contain 2 CPU chips per node with 12 cores/CPU.  Each standard node has a total of 128 GB of available shared RAM.**
![standard](https://github.com/tbrunetti/Rosalind_HPC/blob/master/images/standard_compute_node.png)
**The 2 high memory nodes each contain 2 CPU chips per node with 18 cores/CPU. Each high memory node has a total of 1536 GB of available shared RAM.**
![high_memory](https://github.com/tbrunetti/Rosalind_HPC/blob/master/images/high_memory_compute_node.png)

<div class="paragraph"><p><br>
<br></p></div>

## Accessing/Utilizing the High Memory Nodes
Due to the limited number of high memory nodes, only jobs that surpass the memory requirements of the standard nodes or lack of standard node availability should the user choose to run on jobs on these two designated nodes.

The high memory node can be specified in the SLURM batch script by adding the following line of code to the #SBATCH headers:  
```
#SBATCH -p bigmem
```

This will automatically submit your job to the high memory nodes if there are enough resources available to allocate for the specified job.  If not, your job will wait in the bigmem queue until resource become available for the high memory nodes.

<div class="paragraph"><p><br>
<br></p></div>

## Accessing/Utilizing SAS
Currently, we have 2 standard compute nodes with SAS licenses or (48 CPU/cores available total across the 2 nodes).  There are two ways a user may want to access SAS: interactively or submitting a batch script to a SAS node(s).  

__Interactive SAS__  
SAS can be run interactively on the Rosalind command line as well by running through the following steps.  This is analogous to running SAS in real-time using the SAS command prompt.  
*1.  First request an available SAS node by running the following on the Rosalind command line (note: last character is lowercase L):*
```
srun --time=60 -p sas -n1 --pty bash -l
```
This will request a single SAS node (-n1) for a total of 1 hour (--time=60).  

*2.  Next, type in the following to execute and start the SAS interactive session:*
```
/opt/SAS/9.4/SASFoundation/9.4/bin/sas_en -nodmsexp
```
You are now in an interactive SAS session that will automatically terminate in 1 hour.  However, it is important to note the following:
__terminating an interactive session earlier than the specified time is a 2 step process!__  If you do not follow the 2 step process, you will be charged for the full time specified regardless if you actually used the reserved node.  

*3.  Terminating an interactive session early:*
  * Ctrl-d will terminate SAS
  * another ctrl-d will terminate the interactive session on the SAS node or `scancel <your jobid>` which can be found by `squeue -u <yourusername>`  

To be sure the session is terminated type:
```
sacct
```
You should see that job that has the sas interactive session has a status of COMPLETED or CANCELED


__BATCH SAS__  
*1.  The first step is to specify the batch script should be submitted to a node with a SAS installation.  This can be done by adding the following line to the list of #SBATCH headers:*
```
#SBATCH -p sas
```
*2.  Next, a user may wish to specify the number of SAS nodes they would like to use __(max 2)__ or the number of CPUs/cores they would like to use __(max 24 per node)__.  This should be specified in the #SBATCH headers.*  


*3.  When running the SAS command call in the sbatch script use the following SAS executable call:*
```
/opt/SAS/9.4/SASFoundation/9.4/bin/sas_en <followed by your SAS script>
```

*4.  Keep in mind if a time is not specified in the batch script header, the job will automatically be killed after 4 hours.  However, you can specify a time of up to 1 week for these nodes.*

<div class="paragraph"><p><br>
<br></p></div>

## Accessing/Utilizing MATLAB
MATLAB access is similar to how one would access the SAS node.  Currently, we have 4 standard compute nodes with MATLAB licenses or (96 CPU/cores available total across the 4 nodes).  There are two ways a user may want to access MATLAB: interactively or submitting a batch script to a MATLAB licensed node(s).  

__Interactive MATLAB__  
MATLAB can be run interactively on the Rosalind command line as well by running through the following steps.  This is analogous to running MATLAB in real-time using the MATLAB command prompt.  
*1.  First request an available MATLAB node by running the following on the Rosalind command line (note: the character following the bash - is a lowercase L):*
```
srun --time=60 -p matlab -n1 --pty bash -l
```
This will request a single MATLAB node (-n1) for a total of 1 hour (--time=60).  

*2.  Next, type in the following to execute and start the MATLAB interactive session:*
``` 
/opt/MATLAB/R2017b/bin/matlab
```
You are now in an interactive MATLAB session that will automatically terminate in 1 hour.  However, it is important to note the following:
__terminating an interactive session earlier than the specified time is a 2 step process!__  If you do not follow the 2 step process, you will be charged for the full time specified regardless if you actually used the reserved node.  
*3.  Terminating an interactive session early:*
  * Ctrl-d will terminate MATLAB
  * another ctrl-d will terminate the interactive session on the MATLAB node or `scancel <your jobid>` which can be found by `squeue -u <yourusername>`

To be sure the session is terminated type:
```
sacct
```
You should see that job that has the matlab interactive session has a status of COMPLETED or CANCELED


__BATCH MATLAB__  
*1.  The first step is to specify the batch script should be submitted to a node with a MATLAB installation.  This can be done by adding the following line to the list of #SBATCH headers:*
```
#SBATCH -p matlab
```
*2.  Next, a user may wish to specify the number of SAS nodes they would like to use __(max 4)__ or the number of CPUs/cores they would like to use __(max 24 per node)__.  This should be specified in the #SBATCH headers.*  

*3.  When running the MATLAB command call in the sbatch script use the following MATLAB executable call:*
```
/opt/MATLAB/R2017b/bin/matlab <followed by your MATLAB script>
```

*4.  Keep in mind if a time is not specified in the batch script header, the job will automatically be killed after 4 hours.  However, you can specify a time of up to 1 week for these nodes.*

<div class="paragraph"><p><br>
<br></p></div>


## Accessing longrun queues
The longrun queue can be specified in the SLURM batch script by adding the following line of code to the #SBATCH headers:
```
#SBATCH -p longrun
```
It is __important__ to note that longrun still __requires__ that a time be specified in the #SBATCH headers:
```
#SBATCH --time=4320
```
The above would kill the job after 72 hours or 4320 minutes. SLURM also allows time to be specified in the following formats:
  * minutes (example above)
  * minutes:seconds
  * hours:minutes:seconds
  * days-hours
  * days-hours:minutes
  * days-hours:minutes:seconds
