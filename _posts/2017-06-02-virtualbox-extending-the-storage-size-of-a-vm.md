---
layout: post
title: VirtualBox&#58; Extending the Storage Size of a VM
description: How to extend the storage of a VDI or VHD machine.
image: https://byabbe.se/assets/default.png
tags:
  - tips
---

I spend way to much time in a Virtual Machine, I always give them to little storage and I always find myself searching the web for a solution to increase the storage of a particular VM. This is my attempt to learn it for real once, or at least have all the information in the same place for future my needs.

Note\: this solution only works for VDI/VHD files and before attempting this you should backup your VM.

### VBoxManage

The first of the tools to achieve larger storage is [VBoxManage](https://www.virtualbox.org/manual/ch08.html), you will find it in the root directory of your VirtualBox installation location.

Changing your VMs size to 80GB could be as simple as doing\:

Did I say you should take a backup of your VM?

```
VBoxManage modifymedium /path/to/vm --resize 81920
```

If you are having a bad day and this just throws a error try replacing the path of the VM with its UUID. To list all your VMs and their UUIDs do\:

```
VBoxManage list hdds
```

Now the VM got more logical storage assigned to it but this is usually not given to any existing partition. To resize your VM partitions you could use any of your favorite tools for the task. 

I would suggest using GParted which is available on the installation ISO for Ubuntu. Just boot to it and select the "Try Ubuntu" option. Launching GParted is then as easy as `$ gparted`.
