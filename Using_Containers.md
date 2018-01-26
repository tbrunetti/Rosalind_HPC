# Using Containers on Rosalind


Why use a container?

There are many reasons why someone may want to use a container:
1.  Ensure results are reproducible between and users and systems
2.  Version control of software
3.  Install and pre-compile OS and Software of your choosing without having to have root/administrative access to install software globally on the host system
4.  Containers are mobile and portable between systems and users


<div class="paragraph"><p><br>
<br></p></div>

## Singularity vs Docker
Rosalind directly supports the use of Singularity containers within the HPC environment.  Unfortunately, Rosalind, and in fact, nearly *all* HPCs **do not** support Docker directly due to the security risks (i.e. the ability to become a root user) that is imposes to the HPC environment.

One of the largest differences between Singularity and Docker is that the permissions of a container always equal the same permissions a user has on the host environment (i.e. the environment where the container is being used).  This means a few things:  
1.  Naturally, this means that a user can never have root privileges to their container within the context of the HPC environment, unless you already are granted root/sudo privileges within the HPC environment, which is usually restricted to only a limited number of system administrators.  
2.  This also means, that once a user has "activated" or are using his/her container a user cannot change the privileges within the container to exceed the privileges the user has on the host system.  
3.  Any changes to the container image (i.e. updating code within the image)  *must* be performed on a local computer where the user has root access.

The good news is singularity is compatible with Docker images so a user can still use a Docker image within the context of Singularity.

<div class="paragraph"><p><br>
<br></p></div>

## Singularity

**It is important to know, that _each_ run call you make to the singularity container image is independent of any other calls.  i.e. if you run the container image, it does not carry over or save variables and inputs to the next time you call that same container.**



### Instructions for building a new custom singularity container
As mentioned above, in order to write and permanently modify the contents of a container, one must build the container on a system where the user has root access.

We have written an introductory tutorial of building custom Singularity containers and running them on Rosalind.  For new Singularity users, we urge you to [download the PDF here](https://github.com/tbrunetti/Rosalind_HPC/blob/master/supplemental_PDFs/using_singularity.pdf) and read through it.



### Running a Singularity Container Image on Rosalind

**1.  Cleaning your environment**  
If the container has software that conflicts with software currently loaded within your HPC enviroment, please purge and load the required modules first to ensure the proper version of software in the container is being utilized.
```
module purge
module load slurm/16.05.8
```
Next, load the proper singularity module:
```
module load singularity/2.4.2c
```
All of the singularity commands should now be available for use on Rosalind.  If you would like to submit a singularity run command via the queue/sbatch script please make sure you include all three of the previous commands above within your sbatch script.  

**2.  Binding/Mounting your Container**  

For documnetation please dowload and read through the PDF we have written [here](https://github.com/tbrunetti/Rosalind_HPC/blob/master/supplemental_PDFs/using_singularity.pdf)

**3.  Executing scripts within your container**  

For documnetation please dowload and read through the PDF we have written [here](https://github.com/tbrunetti/Rosalind_HPC/blob/master/supplemental_PDFs/using_singularity.pdf)

<div class="paragraph"><p><br>
<br></p></div>

## Docker

Rosalind, and in fact, nearly *all* HPCs **do not** support Docker directly due to the security risks (i.e. the ability to become a root user) that is imposes to the HPC environment.  However, this is not to say, that a user cannot use a Docker image on the HPC.  In order to use an already existing Docker image, all you need to do is import and wrap it into a singularity container.  For more informtaion on how to do this please visit the Singularity documentaion listed [here](http://singularity.lbl.gov/docs-docker)
