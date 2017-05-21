---
date: 2017-05-15T08:12:27-04:00
subtitle: ""
tags: []
title: Using libvirt to host my VM's.
---

Recently I installed Fedora 25 to test some playbooks and other configurations. A co-worker mentioned to use Vagrat but, my exposure was minimal. I only used vagrant to test some applications such as ```netbox``` and it uses Virtualbox by default. Previously I have used Virtualbox and Vmware but, I decided to move away from those. First, Virtualbox breaks everytime there is a kernel update. Although there is some commands you can run to recreate the kernel it needs but, why I should do that all the time? Second, every time I installed a VM, the usage of the HDD went over 105% in ```atop!```. Vmware is great but, they removed a lot of good features, higher price and getting a license is a pain. After running into this issue, I decided to try out libvirt since I found out in can be used with vagrant. You can start installing libvirt with groupinstall:

```
sudo dnf groupinstall "Virtualization"
```
Installing this extra rpms that are helpful to use.
```
sudo dnf install qemu-kvm virt-install virt-manager
```
Make sure this services are enabled and started
```
sudo systemctl enable libvirtd
sudo systemctl start libvirtd
sudo systemctl enable virtlogd
sudo systemctl start virtlogd
sudo systemctl enable network
sudo systemctl start network
```

Since I wanted to create the VM's and access them over the network, I needed to create a bridge. By default, libvirt creates a network with NAT. This is the steps I took:
```
sudo systemctl stop NetworkManager
sudo systemctl disable NetworkManager
```
You should have an int automatically created when you installed the OS. You can find the name of it by running:
```
ifconfig
ls /etc/sysconfig/network-scripts/
```
In my case it was named ifcfg-eno1. Edit the interface:
```
sudo vim /etc/sysconfig/network-scripts/ifcfg-eno1
# add TYPE=Bridge save and close
```

Restart network services
```
sudo systemctl restart network
```
After a while I lost connection to the network and internet. I restarted ```network``` and got this error ``` Determining IP information for br0.. /usr/sbin/dhclient-script: line 704: /etc/resolv.conf file not found``` I tried to touch the file but, it did not even let me ```permission denied```. After doing ``` ls -laht /etc/resolv.conf``` I noticed that the file was linked to ```/var/run/NetworkManager/resolv.conf``` but, it was missing. By recreating the file at this location and restarting ```NetworkManager``` everything seemed to start working. I restarted ```network``` and ```ping duckduckgo.com``` and got a response! Later, I researched into this issue and turns out you don't have to turn off ```NetworkManager``` anymore. Turning off and disabling ```NetworkManager``` gets rid of the link to ```/var/run/NetworkManager/resolv.conf``` and the ```network``` service cannot resolve without this file.

then check the bridge interfaces
```
brctl show
```
At this point everything should be running and working.

I installed a couple of VM's on the same disk ```/dev/sdc``` and noticed the busy % never went higher than 73. It went back and forth between 55 and 73. To test this again, I used my extra disk that is similar on ```/dev/sdd``:
```
[2:0:0:0]    disk    ATA      WDC WD10EZEX-00B 1A01  /dev/sdc
[3:0:0:0]    disk    ATA      WDC WD10EZEX-00B 1A01  /dev/sdd
```
This is the steps I took:

```
sudo parted /dev/"name of disk" #example /dev/vdb or /dev/sdb

#in the parted menu do ```print ``` to see the disks then do:
mklabel > gpt
mkpart
#name of the disk
#what filesystem to use
# the number of the drive
# the size of the drive in GB
# after this then you format it

 sudo mkfx.xfs /dev/"the drive plus the number" #example /dev/vdb1

#then mount it

sudo vim /etc/fstab
# /dev/vdb1 /data xfs defaults,noatime 0 0
```
I mounted the drive directly without LVM's or anything else. I used ```virt-manager``` and added a pre-formatted block device to store the VM's.


```
lsscsi
[0:0:0:0]    disk    ATA      ST31500341AS     CC1H  /dev/sda
[1:0:0:0]    disk    ATA      ST31500341AS     CC1H  /dev/sdb
[2:0:0:0]    disk    ATA      WDC WD10EZEX-00B 1A01  /dev/sdc
[3:0:0:0]    disk    ATA      WDC WD10EZEX-00B 1A01  /dev/sdd
[4:0:0:0]    cd/dvd  HP       DVD Writer 1260d KH25  /dev/sr0
[6:0:0:0]    disk    ST2000DM 001-9YN164       CC4H  /dev/sde
[6:0:0:1]    disk    ST2000DM 001-9YN164       CC4H  /dev/sdf
```
