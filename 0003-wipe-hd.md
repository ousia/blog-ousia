---
tab: none
title: Wipe an Entire Hard Disk
layout: page
permalink: /0003/
---

When you donate or sell a computer, you should erase the data it contains before giving it.

Formating the hard drive is not enough to make its data unrecoverable. This only erases a small portion of data in your hard disk.

The proper way to do it is to overwrite the whole disk with new data.

## Requirements

All you need is the following:

* The computer with the hard disk to be completely erased.

* An empty USB stick to install a _Linux_ live distribution on it.[^live-usb]

[^live-usb]: Any [_Fedora_](https://getfedora.org/) distribution would do fine. Just in case it might help, I used the latest version of [_Fedora LXDE_](https://spins.fedoraproject.org/lxde/).

	[_Fedora Media Writer_](https://github.com/MartinBriza/MediaWriter/releases/latest) is required to save the image to your USB stick

* 24 hours time to perform the operation.

* A spare room in which you may leave the computer.[^spare-room]

[^spare-room]: My mistake was sitting on the same room where the hard disk was being erased. The fan was working (almost) all the time and this prevented concentration.

The safest way wipe the data of an entire hard disk in _Linux_ is to write random data in the entire hard disk.

There are two methods, one is faster and the other is safer. Writing everything with zeros is faster, but filling everything in the disk with random data is safer.

Although it takes longer, I’m only explaining the method with random data because of its superior safety.

## Automatic Mode

The following commands need to be run as root (otherwise `/dev/hda` will not be available to be written):

```
for n in `seq 7`; do dd if=/dev/urandom of=/dev/sda bs=8b conv=notrunc; done && poweroff
```

The first command (which is actually a loop) will overwrite the entire hard disk with random data.

The second command will shut down the computer after has completed successfully the first command.


## Measured Mode

If you want to measure how much it takes to perform every single disk overwriting and all the data wiping operation, you may want to run as root:

```
time for n in `seq 7`; time do dd if=/dev/urandom of=/dev/sda bs=8b conv=notrunc; done
```

After the operation is performed, all data will be available on the shell.

<!--
## Before You Start

This method works and leaves all data contained in the hard disk beyond recover.

Before proceeding, please take in consideration the following:

1. You don’t need any of the data from the hard drive.

1. You’ve made a backup of the relevant data.

1. Again, once the operation is performed all data in the drive will be lost forever.

	Since all space in the drive is filled with random data seven times, it is impossible to recover the original data from the drive.
	
### Notes
-->