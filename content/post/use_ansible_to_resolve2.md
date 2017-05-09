+++
categories = ["ansible"]
date = "2017-05-08T15:51:12-04:00"
tags = []
title = "Use Ansible to Resolve IT Issues Part 2"

+++
After being able automate user creation/deletion, I tackle on how to automate the Cloudera CM install as much as possible. I ran into issues when I created the postgres user and DB, failing to connect. I forgot that postgres does not let you do this as root and you have to switch to the ```postgres``` user. This is how I was able to resolve it:

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
 I had to become user ```postgres``` then create the user and the password. Then create the DB Cloudera CM will use and give rights to the user.
