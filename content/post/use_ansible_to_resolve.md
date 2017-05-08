+++
categories = []
date = "2017-05-08T13:32:05-04:00"
tags = []
title = "Using Ansible to Resolve IT Issues Part 1"

+++
After I was able to successfully Install Cloudera CM and create a cluster, I was trying to find a way to reduce the deployment time. The current deployments would take too long, waste over 500 of labor hours and no consistency. I could not meet customer demand for new datanodes or clusters and had a reduced workforce due to contract changes. At first I tried to find an all solution like puppet or foreman. But, by installing this two solutions I ran into the same problem with the private name and it was a longer process to get it working. A more troublesome problem was changing the certs for https on Foreman. I also needed to find something that the team can learn fast and able to use. We got into debates going back and forth between ansible and puppet, although none on the team had much experience with Configuration Management. At the end no decision was made and everyone did what they though was easier for them. I decided to learn and use ansible, others kept deploying VM's and configuration manually and others decided to invest more time with ``` shell scripting ```. Using scripts was still a better option but, there was no control or revision on the scripts. Anyone made changes and used the scripts in production making things worse. I went and bought a book on Ansible, Decided to use Gitlab to host all my roles and playbooks.


# Learning Ansible

I have used ansible before in a previous job but, I never created the roles and playbooks. All I did was run the playbooks and manually fix in the servers what failed. My first challenge was getting spacing and indent correctly on the .yaml. That took me a while to learn and understand. Although I read the ansible docs, I did not realize how to format the file correctly. It took me around 20 tries to finally get it correctly.

The first problem as a team was adding users with PKI keys and removing users that left. It was a tedious process:

1. Scp the script to the VM's run ```adduser.sh``` or ```removeuser.sh```
2. We had to do this to every VM when we had a new user or someone left. This was tedious and took us a long time since it was a large number of VM's. Something that could take weeks to 5-8 months depending on the workload.

At first I tried to copy roles that I found in Ansible Galaxy but, I did not understand them right away. I was not able to understand the variables, defaults and how others wrote their roles. I needed something simple that I could learn and be able to teach the rest of the team if the decide to use it. I came across a new acquired customer who started using ansible and had simpler roles I was to understand. So to be able to successfully create new users, I copy and pasted the modules all over the tasks/main.yml for every user I needed. Here is an example:

```
---
  - name: Create Group ""
    group: name=
  - name: Creater user ""
    user: name="" group="" uid="" groups="" expires=""
  - name: Authorized keys ""
authorized_key: user="" key="{{ lookup('file',"dirtothekey/.pub') }}"
```
I copy and pasted this for every user I needed created. My ```main.yml``` was messy and dirty but, I was able to successfully create users with their keys at a fast pace. The whole process of scping every script I needed were long gone. I just had reduced months of work to around 2-3 hours.

After figuring out how add users to the VM's then I needed to figure out how to delete them. To my surprise this was easier than I though. All I needed was:

```
---
  -user:
     name: "gray_cat"
     state: absent
```

that is all! it was so simple, I was speechless! I was able to remove all those customers and co-workers who had left the project. Again, I was able to remove hours wasted on removing users.
