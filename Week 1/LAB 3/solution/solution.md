# Solution To Lab 3 Task

Disks are what azure use to store data, applications and operating systems.

## Default azure disks

There are2 default azure disks:

Operatying System Disk which can be up to 2Tb and hosts the Virtual machine's operating system.

There is also the Temporary Disk which uses a solid-state drive. located on the same azure host as the vm.

## Azure data disks

Azure data disks are appropriate to use for data storage

## VM disk types

Azure provides two types of disks: Standard disks and Premium disks

## Create and attach disks

i created a data disk together with a vm

## Prepare data disks

I prepared the disk by configuring the use to use it.
i started by using ssh to connect to my VM's public address. then i parted the dosk, and mounted it afterwards.

lastly i wrote to the etc/fstab file
