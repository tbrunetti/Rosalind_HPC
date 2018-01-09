# Nodes and Queues Available

# Nodes and Queues Available
Rosalind has a few nodes and queues for which a user can choose to submit a job.  This becomes particularly important if a user requires any of the following specifications:
  * SAS
  * MATLAB
  * large memory requirements > 100GB
  * long run times > 36 hours  

This is because SAS and MATLAB are only currently available on a subset of standard compute nodes, and the default standard compute nodes only have a total of 128 GB of usable RAM. Although all nodes have the capacity to run past 36 hours, SLURM automatically kills any jobs on the standard compute nodes surpassing this time limit unless a specific queue is specified, regarless of the time specified by the user.

## Nodes
By default, if a user does not specify a node type, all jobs are submitted to one or more of the standard compute nodes.  In order to access a high memory node, a user must specify this in the SLURM script.  

Rosalind has two types of compute nodes available for general use:
  *  32 standard compute nodes
  *  2 high memory compute nodes

**The 32 standard compute nodes contain 24 CPUs per node for a total of 128 GB of available RAM per node.**
![standard](https://github.com/tbrunetti/Rosalind_HPC/blob/develop/images/standard_compute.png)
**The 2 high memory nodes contain 36 CPUs per node for a total of 1536 GB of available RAM per high memory node.**
![high_memory](https://github.com/tbrunetti/Rosalind_HPC/blob/develop/images/high_memory_compute.png)

## Accessing/Utilizing the High Memory Nodes
Due to the limited number of high memory nodes, only jobs that surpass the memory requirements of the standard nodes or lack of standard node availability should the user choose to run on jobs on these two designated nodes.

The high memory node can be specified in the SLURM batch script by adding the following line of code to the #SBATCH headers:  
```
#SBATCH -p bigmem
```

This will automatically submit your job to the high memory nodes if there are enough resources available to allocate for the specified job.  If not, your job will wait in the bigmem queue until resource become available for the high memory nodes.


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
