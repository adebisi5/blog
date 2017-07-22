+++
date = "2017-05-08T13:32:05-04:00"
tags = []
title = "Install libvirtd"
+++
Recently I installed Fedora 25 to test some playbooks and other configurations. A co-worker mentioned to use Vagrant but, my exposure was minimal. I only used vagrant to test some applications such as ```netbox``` and it uses Virtualbox by default. Previously I have used Virtualbox and Vmware but, I decided to move away from those. First, Virtualbox breaks everytime there is a kernel update. Although there is some commands you can run to recreate the kernel it needs but, why I should do this all the time? Second, every time I installed a VM, the usage of the HDD went over 105% in ```atop!```. Vmware is great but, they removed a lot of good features, higher price and getting a license is a pain. After running into this issue, I decided to try out libvirt since I found out in can be used with vagrant. You can start installing libvirt with groupinstall:

```
sudo dnf groupinstall "Virtualization"
```
Install this extra rpms.
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

After restarting my server after patches, I lost connection to the internet again. Turns out ```/etc/resolv.conf``` is missing again. I had to do:
```
sudo touch /etc/resolv.conf
sudo systemctl restart network
```
I got connection again and was able to download more ISO's for the server builds. But, this happens every time there is a restart. I reported this issue fedora bugzilla and see if its a bug.

Finally check the bridge interfaces.
```
brctl show
```
At this point everything should be running and working. I created my VM's using ```virt-manager``` and tested some ansible roles.

NOTE: I decided to reinstall my OS and try to use software RAID 1 for everything. Using the HDD's I have available below and performance has been great.

```
[2:0:0:0]    disk    ATA      WDC WD10EZEX-00B 1A01  
[3:0:0:0]    disk    ATA      WDC WD10EZEX-00B 1A01  

```
