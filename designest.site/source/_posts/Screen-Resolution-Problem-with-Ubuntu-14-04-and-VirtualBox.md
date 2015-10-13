title: Screen Resolution Problem with Ubuntu 14.04 and VirtualBox
date: 2015-10-13 20:09:51
tags: VirtualBox
categories:
 - Issues
---
I have VirtualBox 5.0.6 installed on Windows 10 host.
And I have decided to create new VM, in other words, I have installed Ubuntu 14.04 64-bit as guest operating systems by using VM Virtual Box. 

# Issue

I have found that I can't change Screen Resolution on my new VM.

# Resolving

On VirtualBox you have to install "Guest Additions". There is no need to set a resolution via Ubuntu settings. From your guest window of VirtualBox select
```
Devices -> Insert Guest Additions CD image
```

In Ubuntu open a terminal, navigate to cd folder (usually /media/some-user/VBOXADDITIONS*) and run
```
sudo sh ./VBoxLinuxAdditions.run
```

Then shutdown you VM and restart VirtualBox.

