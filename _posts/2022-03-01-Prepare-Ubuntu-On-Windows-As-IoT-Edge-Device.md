---
layout: post
title: How to prepare the Ubuntu created by Hyper-V to be a Azure IoT Edge device 
description: Step by step instruction on how to prepare Ubuntu to be a Azure IoT Edge Device.
tags: 
- azure
- azure-iot
- azure-iot-edge
- hyper-V
- ubuntu
---

# Create Unbunt VM using Hyper-V quick create

- Open Hyper-V Manager, select Quick Create

![Hyper-V Quick Create](/public/image/HyperVQuickCreate.png "Hyper V quick create")

- Select *Ubunto 20.04*

![Hyper-V Quick Create Ubuntu](/public/image/HyperVQuickCreateUbuntu2004.png "Hyper V quick create ubuntu")

Depends on your internet connection, it is going to take awhile

![Hyper-V Quick Create Ubuntu Progress Bar](/public/image/HyperVQuickCreateUbuntu2004ProgressBar.png "Hyper V quick create ubuntuProgress bar")


![Hyper-V Quick Create Ubuntu Successful](/public/image/HyperVQuickCreateUbuntu2004Successful.png "Hyper V quick create ubuntuProgress bar")

- Click *Edit Settings...*
![Hyper-V Quick Create Ubuntu Successful](/public/image/HyperVQuickCreateUbuntu2004ExpandDisk.png "Hyper V quick create ubuntuProgress bar")
 Give enough disk space (>100GB) to the virtual machine. 

 - Connect to the VM

 Please follow the [instruction](/_posts/2022-03-02-How-To-Increase-DiskSpave-Of-Ubuntu-On-HyperV.md) on this post to expand the disk in Ubunto the all the disk space just allocated

 - Update all the components.

 Most likely when you installed the VM, some of the components are outdated

 ```
 sudo apt install update

```

This will update all components to the latest.

- Enable SSH server

Sometime you don't want to connect to the VM using Hyper-V, instead tools like Putty is preferred. In this case, the SSH server needs to be installed on the VM

 ```
 sudo apt update
 sudo apt install openssh-server
 ```

 Once the installation is complete, the SSH service will start automatically. You can verify that SSH is running by typing
 ```
 sudo systemctl status ssh
 ```

 Press `q` to get back to the command line prompt

 Ubunto shipped with Firewall configuration tool called UFW. make sure SSH port is allowed in the Firewall
 ```
 sudo ufw allow ssh
 ```
 