+++
categories = []
date = "2017-05-08T11:52:33-04:00"
tags = []
title = "Big Data on Openstack Part 1"

+++
Openstack can be a great solution due to the increase demand of  cloud and more resources. But, it can't resolve every issue out there. an Openstack deployment can provide "unlimited" resources but, is useless if is not architectured for the specific applications that the VM's will be hosting. For example, a previous customer had over 20 regions, configured almost the same and had performance issues. This  customer hosted big data applications (Cloudera to be specific) on those VM's, had an older deployment of Openstack ( Icehouse so we could not take advantage of the newer cloud features) and no budget for further expansion and upgrades ( Including software and hardware) but, had the following issues:

1. Was forced to use Centos 6/7. No budget for OS support.
2. Cloudera Clusters could not talk to each other from different regions.
3. Adding extra datanodes to a cluster using resources from a different region was not possible. Customer had to create a new cluster in every region.
4. Application links inside Cloudera CM would fail to resolve.
5. A new Cloudera Cluster would take around 2-5 months to deploy due to loosing knowledge ( employees left the project) and configuration issues.

I tried following the little documentation the previous Sys Admin had left but, that was troublesome. I had to spend significant time researching on the internet to find solutions to some of the issues I came across. At first I tried building a 5 host cluster with Centos 6. But, the installation would fail due to the Cloudera CM not able to talk to the cloudera agent( they were on the same host!). I found out later that is a bug with Cloudera CM with Cloud Solutions such as AWS/Openstack due to the way Openstack networking works (Floating/Public /Private hostname & IP) (https://www.cloudera.com/documentation/enterprise/release-notes/topics/cm_rn_known_issues.html) Basically this:

```
Installing on AWS, you must use private EC2 hostnames.

When installing on an AWS instance, and adding hosts using their public names, the installation will fail when the hosts fail to heartbeat.

Severity: Med

Workaround:

Use the Back button in the wizard to return to the original screen, where it prompts for a license.

Rerun the wizard, but choose "Use existing hosts" instead of searching for hosts. Now those hosts show up with their internal EC2 names.

Continue through the wizard and the installation should succeed.
```

Since Openstack operates similar to AWS then I figure I was running into this same issue. I was able to fix it by:

1. Either use all private hostname in ``` /etc/hostnames ``` and ``` /etc/hosts ```. Yes, the name Openstack injects when you create a VM and give it a name. For example, ```cloudera-cm-$regionname``` or use all FQDN. Using the private hostname in all the VM's worked but, they still could not reach nodes in another region and Cloudera CM would inject the
private hostname in all the links it provided in the UI. For example, if you decided to bring up the Namenode Http page from the UI, instead of resolving, it will fail because it would open ```https://cloudera-cm-$regionname:50070``` instead of the FQDN( obviously it will not resolve since DNS does not know that name). This became an issue since customers would try to use the UI and complain that Cloudera is down because the page will not come up. This was resolved by using The Floating IP or the FQDN (every IP already had a FQDN in DNS) ```https://bigdata.cloud.example.com:50070/``` (Told customers to just bookmark this link and ignored the links in the UI). This same problem happened with all big data applications. HDFS, Solar,Hue, Impala etc. I created another cluster to test using FQDN in all the nodes but, the install failed. So I had to go back to using the private names.

I continued testing ways to fix it but, it became more conversome. I decided to try with Centos 7 since I been using it more than 6. Using centos 7 made it easier to make certain configurations due to some tools:

1. nmtui - Using nmtui changed the hostname in all the right locations and the cloudera installer accepted it right away( after a reboot)
2. hostnamectl - Using hostnamectl was another option that changed the hostname correctly. ```hostnamectl set-hostname cloudera-cm-mars1.z1```

I did not go into extra research to see what other tools would work on centos 6 and switched to 7 since it reduced the time needed to deploy a cluster ( shaved off around an hour or so of troubleshooting).

While researching more issues and stalking the cloudera forums, I came across how cloudera figures out the hostname. It runs this python command:

```
python -c "import socket;print socket.getfqdn();
print
socket.gethostbyname(socket.getfqdn())"
```
Regardless what I try, this command will always resolve to the private name. To summarize, I was able to get Cloudera CM installed doing the following:

1. Install in Centos 7 due to the new tools and new updates.
2. Use ```nmtui``` and ```hostnamectl``` to change the name of the system to the private hostname then restart. always use the private name.
3. All the VM's will have to be on the same project and region. Adding from other regions can be a hit & miss. This can be annoying but, the only solution I was able to find.
4. I was able to discover that this issue in Openstack is not only with Cloudera CM or Hadoop but, tons of other applications. Elasticsearch,Puppet and foreman to name a few. The troublesome install of Puppet and Foreman was what direct me to use Ansible.
