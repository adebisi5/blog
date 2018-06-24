+++
categories = ["ansible"]
date = "2017-05-08T13:32:05-04:00"
tags = []
title = "Using Ansible to Resolve IT Issues Part 1"

+++
After spending months on trying to deploy a Cloudera CM cluster with over 40 nodes, I needed to find a way automate most of my tasks and reduce time spend doing this manually. At the time when I started on this project we were using openstack VM's to host this Cloudera cluster. Although is not best practices to use VM for big data, it was our only option of having resources. Being new to the team and trying to find all the documentation and scripts that were used by the previous team member was a challenge. After spending some time researching, I came across some scripts and documentation. Although they were mostly outdated, I was able to used some of to reduce some of the work. What made it a bigger challenge was the fact of the continous increase for more datanodes to be used by our customer and tight deadlines. We needed to find a way to automate more because the current process was not cutting it. At the time the organization was heavy on using puppet. As I tried to learn puppet it became a challenge just for the fact that it has a bigger learning curve, a challenge trying install this software on openstack VM's and have it use the correct FQDN and not the internal name. The other issue was that I had thousands of VM's in different regions and have it communicate to the puppet master was a challenge. I also needed to find something that anyone can learn pretty quick since most of my co-workers were doing tasks manually and not using some form of Configuration Management( they used .sh but, still it was a pain). I discussed this more with my team but, no decision was made since no one was familiar with anything. I had been exposed to ansible before but, I never wrote any roles or playbooks. I was just intructed to run a playbook and that is all I did. I gave puppet once more change and still came across the same issues. I just decided to checkout ansible since I started to see it mentioned more in reddit. I also got an ansible book so I have another reference in my learning experience.

# Learning Ansible

I have used ansible before in a previous job but, I never created the roles and playbooks. All I did was run the playbooks and manually fix in the servers what failed. My first challenge was getting spacing and indent correctly on the .yaml. That took me a while to learn and understand. Although I read the ansible docs, I did not realize how to format the file correctly. It took me around 20 tries to finally get it correctly.

Like mentioned before we did a lot of the work manually or running scripts. The scripts helped but, image `scp` the same scripts over thousands of servers? :( although that was a big challenge I was trying to figure out what I can automate or write successfully with ansible since I still had no idea what I was doing. The first problem we experience is adding and removing team members on the VM's. It was a tedious process.

1. Scp the script to the VM's run ```adduser.sh``` or ```removeuser.sh```
2. We had to do this to every VM when we had a new user or someone left. This was tedious and took us a long time since it was a large number of VM's. Something that could take weeks to 5-8 months depending on the workload.

At first I tried to copy roles that I found in Ansible Galaxy but, I did not understand them right away. I had no idea or understanding on the directory structure.I also did  not o understand the variables, defaults and how others wrote their roles. I needed something simple that I could learn and be able to teach the rest of the team if the decide to use it. I came across a new acquired customer who started using ansible and had simpler roles I was to understand. So to be able to successfully create new users, I copy and pasted the modules all over the tasks/main.yml for every user I needed. Here is an example:

```
---
  - name: Create Group ""
    group: name=
  - name: Creater user ""
    user: name="" group="" uid="" groups="" expires=""
  - name: Authorized keys ""
authorized_key: user="" key="{{ lookup('file',"dirtothekey/.pub') }}"
```
I copy and pasted this for every user I needed created. My ```main.yml``` was messy and dirty but, I was able to successfully create users with their keys at a fast pace. The whole process of scping every script I needed were long gone. I just had reduced months of work to around 2-3 hours. After figuring out how add users to the VM's then I needed to figure out how to delete them. To my surprise this was easier than I though. All I needed was:

```
---
  -user:
     name: "gray_cat"
     state: absent
```
that is all! it was so simple, I was speechless! I was able to remove all those customers and co-workers who had left the project. Again, I was able to remove hours wasted on removing users.
