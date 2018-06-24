---
title: "Ansible OSP Modules"
date: 2018-01-08T14:00:24-05:00
subtitle: ""
tags: [ansible,osp,cloud]
---

Recently I started working on a project to create roles using ansible openstack modules. I have used openstack before but, the version I used was from 2014 and we managed the VM's/Applications using supernova. We managed VM's for customers in openstack but, we did not maintain the infrastructure itself. Although we troubleshooted and help diagnosed some issues with the openstack team. Issues like a VM got stuck, can't connect to the VM' and having performance issues. At this same time is when I started using  Ansible to manage OS level tasks. For more background on this look at " ". 

I started looking at the [ansible osp modules](http://docs.ansible.com/ansible/latest/list_of_cloud_modules.html#openstack) and thought they were very straight forward to use. Until I ran into the whole cloud.yml and auth dictionary. I assumed ( not sure why) that by connecting with enough permissions I should be able to run this modules and since I have not learned about the latest changes osp since I used an old one.( this project was osp 12). After doing a quick google search I ran into the cloud.yml and it made sense right away. Having the cloud.yml makes it more easier to authenticate and use the osp resources than using the auth dictionary. While both options are great, with the cloud.yml you don't have to include any sensitive information and just point to it on your tasks. This took me a while to figure out because I did not have that exposure of the openstack cli and was using supernova to do similar tasks. After finding this out everything else became easier to figure out and test. First I tested creating a domain, a VM then doing some actions of the VM ( restart or pause).
