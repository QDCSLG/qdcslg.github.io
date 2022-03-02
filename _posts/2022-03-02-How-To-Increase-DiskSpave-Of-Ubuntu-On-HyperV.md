---
layout: post
title: How to increase the diskspace after Ubuntu VM using Quick create by Hyper-V 
description: By default, when creating a Ubuntu VM on Hyper-V machine, one 10Gb of the disk is available. It is not enough
tags: 
- azure
- azure-iot
- hyper-V
- ubuntu
---



Creating Ubuntu VM on Windows Hyper-V environment is pretty easy. However, if this method is used, you may end up with a tiny Ubuntu virtual disk that will not be useful for any serious work and it is less obvious than the initial setup how to increase the size of this disk.

These steps fix the problem:

1. Turn off the VM.
2. Use Hyper-V Manager to select the Settings of the Virtual Machine, select the Hard Drive option and Edit under Virtual hard disk. (If this option is disabled, you need to go back and delete any checkpoints for the VM in the Hyper-V Manager; just select the VM and right click the checkpoint in the checkpoint field below.)
3. Use the GUI to expand the drive to something reasonable, like 128 GB. Ubuntu now has space to expand into.
4. Start the VM again. Install Guest Utils:
    ```
    sudo apt install cloud-guest-utils
    ```
1. If not using English, override locale settings to avoid issues with non-English locales:
    ```
    LC_ALL=C
    ```
1. Expand the sda1 partition into the free space:
    ```
    sudo growpart /dev/sda 1
    ```
    (Note ***the space between sda and 1!***)
1. Finally run resize2fs:
    ```
    sudo resize2fs /dev/sda1
    ```
    (***No space between sda and 1 here!***)
    
Now your Ubuntu drive is 128 GB.