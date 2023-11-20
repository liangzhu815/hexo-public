---
title: roaming-profile
date: 2023-11-17 16:00:48
tags: 
- nfs 
- roaming-profile 
- ldap
---


you login to your desktop with the same credentials as you do our clusters.

i.e. if you login to santa/santa3 like this...
ssh user@santa.bii.a-sta.edu.sg
with the password password.

then on the desktop you also login as
user
with the password password.


notice we say cluster.
that is because your desktop authenticates to the same source of truth as our clusters, and actually mounts the same home directory.
if you login to santa or santa3, you will find that the $HOME is the same $HOME as your desktop.
since we were going to make your desktop auth there, and also use the same nfs home. we also gave u access to all thew queues on santa and all the partitions on santa3.


next thing is the catch.
you do not have sudo on this pc.
we have installed nvidia-535 drivers on it already.
if you need to muck with the kernel let us know. email systems.
most of the time we can ssh to your pc and do something.

we have also installed
distrobox
https://github.com/89luca89/distrobox ,
podman and apptainer (nee singularity)
(and both snap and flatpak. )


i.e. you can

distrobox create $boxname
distrobox enter $boxname
and do your
sudo apt install blah
or 
sudo yum install blah
to your heart's content in your own boxen.
nothing is stopping you (probably?) until you try to muck with the kernel on the underlying os on which you do not have sudo.
you can of course also do anything related to rootless podman.
you can ask podman nicely to run docker images too...i think...
and you can roll your own sif images
which you can leave in your $HOME
then go santa, santa3 to submit jobs that run those sif images.
maybe you'll figure out how to export your podman containers(distrobox is a wrapper; it calls podman. it can also call docker n lilipod but we havent installed them on this machine. rootless podman is already troublesome enough.) and then build sif images out of them...
then you can scale...ibqueue2 on santa and all the santa3 nodes have singularity installed.

er...we also put micromamba in usr local bin. and softlinked "conda" to it.
so you can use conda already too(conda forge is in the system wide mambarc).
or you can get condaforge/miniforge yourself, your condarc takes precedence over the system wide mambarc...
and um. make sure your conda is in front of /usr/local/bin in your PATH...yes let us know if mamba is not an acceptable replacement for conda for you and you have difficulty with exporting $PATH
