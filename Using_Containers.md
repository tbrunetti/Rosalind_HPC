# Using Containers on Rosalind

What is a container?

Why use a container?

<div class="paragraph"><p><br>
<br></p></div>

## Singularity vs Docker
Rosalind directly supports the use of Singularity containers within the HPC environment.  Unfortunately, Rosalind, and in fact, nearly *all* HPCs **do not** support Docker directly due to the security risks (i.e. the ability to become a root user) that is imposes to the HPC environment.

One of the largest differences between Singularity and Docker is that the permissions of a container always equal the same permissions a user has on the host environment (i.e. the environment where the container is being used).  This means a few things:  
1.  Naturally, this means that a user can never have root privileges to their container within the context of the HPC environment, unless you already are granted root/sudo privileges within the HPC environment, which is usually restricted to only a limited number of system administrators.  
2.  This also means, that once a user has "activated" or are using his/her container a user cannot change the privileges within the container to exceed the privileges the user has on the host system.  
3.  Any changes to the container image (i.e. updating code within the image)  *must* be performed on a local computer where the user has root access.


<div class="paragraph"><p><br>
<br></p></div>

## Singularity


<div class="paragraph"><p><br>
<br></p></div>

## Docker

Rosalind, and in fact, nearly *all* HPCs **do not** support Docker directly due to the security risks (i.e. the ability to become a root user) that is imposes to the HPC environment.  However, this is not to say, that a user cannot use a Docker image on the HPC.  In order to use an already existing Docker image, all you need to do is import and wrap it into a singularity container.  For more informtaion on how to do this please visit the Singularity documentaion listed [here](http://singularity.lbl.gov/docs-docker)
