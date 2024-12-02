---
layout: post
title: "Linux File Sys Read ONly bug"
date: 2024-11-25
---

# Linux下挂载的硬盘变为只读
## 基本原因：

参考[file read only](https://blog.csdn.net/JOHNCHANGE/article/details/103280064)

## 过程：
可能是重启导致的windows什么文件没有写好，所以重新启动ubuntu之后，硬盘里还有win的启动文件被读到了

解决：
图形化界面，修复文件系统

Update：有可能修复失败，我遇到的错误是什么quark错误，但是这个也没找到好的方法解决，但是下面这个方法解决了我的问题，可以试一下
1. lsblk，查看挂载点：
```bash
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
loop0         7:0    0     4K  1 loop /snap/bare/5
loop1         7:1    0  63.3M  1 loop /snap/core20/1828
loop2         7:2    0  73.9M  1 loop /snap/core22/1663
loop3         7:3    0    46M  1 loop /snap/snap-store/638
loop4         7:4    0  63.7M  1 loop /snap/core20/2434
loop5         7:5    0 346.3M  1 loop /snap/gnome-3-38-2004/119
loop6         7:6    0  91.7M  1 loop /snap/gtk-common-themes/1535
loop7         7:7    0  38.8M  1 loop /snap/snapd/21759
loop8         7:8    0  12.2M  1 loop /snap/snap-store/1216
loop9         7:9    0 349.7M  1 loop /snap/gnome-3-38-2004/143
loop10        7:10   0  44.3M  1 loop /snap/snapd/23258
loop11        7:11   0 505.1M  1 loop /snap/gnome-42-2204/176
sda           8:0    0 931.5G  0 disk 
├─sda1        8:1    0 930.8G  0 part /media/chz/63BC5052BA77FA02
└─sda2        8:2    0   736M  0 part 
nvme0n1     259:0    0 931.5G  0 disk 
├─nvme0n1p1 259:1    0   100M  0 part /boot/efi
├─nvme0n1p2 259:2    0    16M  0 part 
├─nvme0n1p3 259:3    0 600.6G  0 part 
├─nvme0n1p4 259:4    0   191M  0 part 
├─nvme0n1p5 259:5    0  15.3G  0 part [SWAP]
├─nvme0n1p6 259:6    0 143.1G  0 part /
├─nvme0n1p7 259:7    0 171.7G  0 part /home
└─nvme0n1p8 259:8    0   736M  0 part
```

我的/media磁盘是挂载在sda/sda1

2.sudo ntfsfix /sda/sda1 #修复这个挂载点

3.sudo mount -o rw /sda/sda1 /mnt/sda1# 重新挂载

## 亲测有用！

