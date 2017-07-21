---
categories = ["ansible"]
date: 2017-05-09T12:03:11-04:00
subtitle: ""
tags: []
title: Using Ansible Tower
---

So you have an idea what is ansible and what you can do with it. After creating, playbooks & roles and dynamic inventories, you are wondering how you can centralize and control access to your playbooks. You can do this with ansible core and limit access and permissions on the git project. You can include all the playbooks, roles and inventory files in the same repo. But, this can become a problem once the project is ``` git clone ``` into the controller and anyone access to the server can potentially be able to access your playbooks. Tower pushes all this files to be more centralized and be controlled with organizations and teams. By using this structure you can limit access to your playbooks and inventory with very specific permissions. For example, you can team A be able to deploy playbooks that create EC2 host but, team B does not have access to those roles. You can actually create teams like actual departments in your company (organization) and limit access by their actual roles (job description). Tower also limits access to this file since they are stored in the database and not easily accessed like ansible core or tower 3.0. So when you start adding credentials this will become private and everyone that tries to look at the credentials will get a ```%encrypted``` and will be able to see anything.
