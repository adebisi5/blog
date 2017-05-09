+++
categories = ["ansible"]
date = "2017-05-08T15:51:12-04:00"
tags = []
title = "Use Ansible to Resolve IT Issues Part 2"

+++
After being able automate user creation/deletion, I tackle on how to automate the Cloudera CM install as much as possible. I first started trying to install the rpms with ansible. I discovered the yum and repo modules. They allow me to add a repo and install any rpm available. This what I have:

```
- name: Add the cloudera-cm repo.
  yum_repository:
    name: cloudera-cm
    description: cloudera-cm repo
    baseurl: "{{ rpm_repo }}" # http://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.11/
    gpgcheck: yes
    gpgkey: "{{ gpg_key }}"
    enabled: yes

- name: update system # Just update the whole system to latest rpms
  yum:
    name: '*'
    state: latest

- name: install packages
  yum:
    name: "{{ packages }}" # wget,net-tools,python,vim,postgresql-server,java,mod_ssl,httpd,MySQL-python,fuse-libs
    state: latest

- name: install cloudera packages
  yum:
    name: "{{ cloudera_rpm }}" # cloudera-manager-agent,cloudera-manager-daemons,cloudera-manager-server
    state: latest
```
Previously doing this process took around 30 minutes to around 2 hours since I had to manually do this to all the potential Cloudera CM's.

I ran into issues when I created the postgres user and DB, failing to connect. I forgot that postgres does not let you do this as root and you have to switch to the ```postgres``` user. This is how I was able to resolve it:

Init the DB first
```
- name: init postgresql
  become: True
  become_user: postgres
  command: '{{ pg_initdb_command }}' # the command is initdb -D /var/lib/pgsql/data
  ignore_errors: yes
  ```

  Then create the user and DB
  ```
  - name: create the postgres user and set the password
    postgresql_user:
     name: "{{ postgres_username }}" # DB user
     password: "{{ postgres_password }}" # DB passwd
     become: True
     become_user: postgres

-  name: create the postgresql database for Cloudera CM
   postgresql_db:
     name: "{{ postgres_database }}" # just the DB name
     owner: "{{ postgres_username }}" # the DB user created above
     state: present
     login_user: postgres
   become: True
   become_user: postgres
```
 I had to become user ```postgres``` then create the user and the password. Then create the DB Cloudera CM will use and give rights to the user. To get the DB finalized, you need to run ```/usr/share/cmf/schema/scm_prepare_database.sh postgresql scm scm scm```. I used a variable to make the ```task/main.yml``` easier to read. This command indicates the type of DB to be used, the user and passwd.

```
 - name: Run the db script to configure for Cloudera CM
  shell: "{{ prepare_database }}" # includes the command above.
```

If you want to see the whole role, check it out at https://gitlab.com/sysadminonlinux/cloudera-cm
