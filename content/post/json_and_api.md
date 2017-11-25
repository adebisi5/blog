---
title: "Json and API"
date: 2017-10-26T22:39:57-04:00
subtitle: ""
tags: [JSON,API]
---

#JSON and API

I started using Vagrant for a while to be able to spin VM's and troubleshoot or test certain configuration. For the moment I was fine with using virtualbox but, I decided to use libvirtd since I prefer it. I had no idea how to create images or where to start. I asked a co-worker and he mentioned to look at bento and packer. Bento has a whole list of json files for images in all linux flavors and builds the images for all Virtualization types. I started trying to use the bento images and they are great for a default installation. But, it gets trickier when trying to make changes to the JSON file if you are not used to JSON format. I wanted to create a JSON file where it uses all the standard config in bento but, it provisions the system with ansible playbook. The tricky part is that ansible needs to be installed in the VM before it can run the playbooks. You can either use the scripting part to install ansible or include it on the the kickstart file. I have not messed around with ks files much before but, so far using the scripting works.




# API

All this time working in IT and I kept hearing "API and rest changes" but, still had no idea the purpose or the advantages of using it. I did not get real exposure until a few years ago when I was supporting a development team. This team had Django applications and I learned how certain parts work.



After getting exposed to ansible then I learned about Ansible Tower. A full django application with a complete Rest API. 


After working with different customers, they decided to use different options:

* tower-cli -
* curl -
* uri module -



After messing around with curl for a while then I learned more about GET, PUT and PATCH.

* PUT - Replaces the resource completely.
* PATCH - Does an update of a specific section without replacing the whole resource.
