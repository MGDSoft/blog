---
layout: post
read_time: true
show_date: true
title:  Vagrant resize box 
date:   2022-11-14 13:32:20 -0600
description: Vagrant resize box for vagrant
img: assets/img/posts/vagrant-logo.png
tags: [vagrant,wsl]
author: Miguel García Domínguez
github:  MGDSoft/blog/
mathjax: yes
---

If you want to resize your vaggrant box you have to follow this simple steps:

```bash
    VBoxManage.exe clonehd "C:\Users\maka5\VirtualBox VMs\seco-start-2_dev_1668463064644_25176\box.vmdk" "C:\Users\maka5\VirtualBox VMs\seco-start-2_dev_1668463064644_25176\out.vdi" --format VDI
    VBoxManage.exe modifyhd "C:\Users\maka5\VirtualBox VMs\seco-start-2_dev_1668463064644_25176\out.vdi" --resize 40360
```

go inside the vagrant box and 

```bash
    resize2fs /dev/device 
```
    
    
