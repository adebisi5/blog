---
title: "Tower Cli"
date: 2017-10-05T12:51:46-04:00
subtitle: ""
tags: [ansible]
---

Tower-cli is a FOSS sofware made to manage Ansible Tower Configuration and launching jobs. Its a tool that communicates using the API and makes it easier to make those changes instead of using curl. Here is an example of things you can change or do with tower-cli:

* Create Users
* Create Organizations
* Create Teams
* Create 
* Launch Jobs
* Change Any configuration found in /api/v1/settings/all
* Orchestrate with other tools and have more complete automation
* CD/CI pipeline


### Example Videos
Ansible Tower: Change a setting with tower-cli (https://youtu.be/gx1We755O1Q)



# Examples:
```
Tower-cli setting modify AUTH_LDAP_SERVER_URI "ldap://ldap.redhat.com:3268"

tower-cli setting modify AUTH_LDAP_SERVER_URI @server_uri

tower-cli setting modify AUTH_LDAP_SERVER_URI "ldap://ldap.redhat.com:3268";tower-cli setting modify AUTH_LDAP_BIND_DN "CN=ansible,OU= Accounts,OU=Information Technology,OU=Administration,OU=United States,DC=fedora,DC=red,DC=redhat,DC=com" ;tower-cli setting modify AUTH_LDAP_BIND_PASSWORD "tower"; tower-cli setting modify AUTH_LDAP_START_TLS "false"; tower-cli setting modify AUTH_LDAP_GROUP_TYPE "ActiveDirectoryGroupType"; tower-cli setting modify AUTH_LDAP_REQUIRE_GROUP "CN=APP_APG0_Users,OU=Global Groups,OU=Accounts,DC=fedora,DC=red,DC=redhat,DC=com"

tower-cli organization create -n kablam -d "the kablam show"
```

They are currently certain configurations that error out if you try to change it with tower-cli so the other option is to use curl or the uri module to make the changes (bug issue is listed here (https://github.com/ansible/tower-cli/issues/352) Here are other examples:

```
- name: get tower tower-auth-token

 uri:

    url: "{{ auth_token_link }}"

    validate_certs: false

    method: POST

    body_format: json

    body: "{\"username\":\"{{ username }}\",\"password\":\"{{ password }}\"}"

    register: login_info

curl -k --basic -u admin:yoursupersecretpasswordgoeshere -i -H "Content-Type: application/json" -X POST  https://${towerhost}/api/v1/job_templates/${jobid1}/survey_spec/  -d @$(pwd)/files/provision-surveyspec

curl -f -k -H 'Content-Type: application/json' -XPOST \
   --user admin:awxsecret \
   http://192.168.42.100/api/v1/job_templates/1/launch/

curl -f -k -H 'Content-Type: application/json' -XPOST \
   -d '{"extra_vars": "{\"foo\": \"bar\"}"}' \
   --user admin:awxsecret http://192.168.42.100/api/v1/job_templates/1/launch/

curl -k --basic -u user:passwd -i -H "Content-Typejson" -X GET https://localhost:8043/api/v2/settings/ldap/
```
