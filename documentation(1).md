#     **IMPLEMENTATION JOURNAL \- LDAP server setup**

 

| Submitted By | Pradeep Singh |
| :---- | :---- |
| Submitted To | Vipin Tripathi |
| Test Case Version | 1 |
| Reviewer  Name | Moumita Roy |

**Goal :**  To set up an LDAP server inside a Podman container on a Linux system, configure user management using an LDIF file, perform user operations (add, delete, search), and integrate it with an Apache web server to create a UI that displays user details.

       Test Environment : 

* OS: Linux (Ubuntu)  
* Container Platform: Podman  
* LDAP Server: 389 Directory Server  
* Web Server: Apache   
* UI: 389ds Cockpit

**Table of Contents**

[**Step 1: Install the packages required	2**](#step-1:-install-the-packages-required)

[**Step 2:  Run the setup utility	2**](#step-2:-run-the-setup-utility)

[**Step 3: Start and Enable the service	3**](#step-3:-start-and-enable-the-service)

[**Step 4: create base.ldif file	3**](#step-4:-create-base.ldif-file)

[**Step 5: create organizational unit	4**](#step-5:-create-organizational-unit)

[**Step 6: verify ldap server running	4**](#step-6:-verify-ldap-server-running)

[**Step 7: create user	6**](#step-7:-create-user)

[**Step 8: add the user in the ldap server	7**](#step-8:-add-the-user-in-the-ldap-server)

[**Step 9: create UI for ldap( install cockpit)	8**](#step-9:-create-ui-for-ldap\(-install-cockpit\))

[**Step 10: start cockpit	8**](#step-10:-start-cockpit)

[**Step 11: verify the cockpit running	8**](#step-11:-verify-the-cockpit-running)

[**Step 11: Access cockpit	9**](#step-11:-access-cockpit)

### 

#### Step 1: Install the packages required  {#step-1:-install-the-packages-required}

| sudo apt install 389\-ds base \-y |
| :---- |

#### Step 2:  Run the setup utility {#step-2:-run-the-setup-utility}

| Sudo dscreate interactive |
| :---- |

This will guide you through the setup process, where you'll define:

* Instance name

* Directory Manager password

* Ports (default is **389** for LDAP and **636** for LDAPS)

#### Step 3: Start and Enable the service {#step-3:-start-and-enable-the-service}

| sudo systemctl enable \--now dirsrv@slapd-test |
| :---- |

Output:

| ○ dirsrv@slapd-test.service \- 389 Directory Server slapd-test. 	Loaded: loaded (/usr/lib/systemd/system/dirsrv@.service; enabled; preset: enabled)	Drop-In: /usr/lib/systemd/system/dirsrv@.service.d         	└─custom.conf |
| :---- |

#### Step 4: create base.ldif file  {#step-4:-create-base.ldif-file}

| nano base.ldif |
| :---- |

This file contains **LDAP object definitions**, such as organizational units, users, and groups.

Output: 

| dn: dc=example,dc=comobjectClass: topobjectClass: domaindc: exampledn: ou=users,dc=example,dc=comobjectClass: organizationalUnitou: users |
| :---- |

#### Step 5: create organizational unit {#step-5:-create-organizational-unit}

| nano ou.ldif |
| :---- |

This file is used to define **Organizational Units (OU)** and other directory entries in **389 Directory Server.**

Output:

| dn: ou=users, dc=example, dc=comobjectClass: OrganizationalUnitou:users |
| :---- |

#### Step 6: verify ldap server running {#step-6:-verify-ldap-server-running}

| ldapsearch \-x \-H ldap://localhost \-D "cn=Directory Manager" \-w Redhat@123 |
| :---- |

Output:

| \# extended LDIF\#\# LDAPv3\# base \<\> (default) with scope subtree\# filter: (objectclass=\*)\# requesting: ALL\#\# example.comdn: dc=example,dc=comobjectClass: topobjectClass: domaindc: example\# users, example.comdn: ou=users,dc=example,dc=comobjectClass: topobjectClass: organizationalUnitou: users\# pradeep, users, example.comdn: cn=pradeep,ou=users,dc=example,dc=comobjectClass: topobjectClass: nsPersonobjectClass: nsAccountobjectClass: nsOrgPersonobjectClass: posixAccountcn: pradeepdisplayName: PradeepgidNumber: 10homeDirectory: home/ldapuid: 11uidNumber: 11\# hareshh, users, example.comdn: cn=hareshh,ou=users,dc=example,dc=comobjectClass: topobjectClass: nsPersonobjectClass: nsAccountobjectClass: nsOrgPersoncn: hareshhcn: harishdisplayName: haresh singh\# ravi, users, example.comdn: cn=ravi,ou=users,dc=example,dc=comobjectClass: topobjectClass: nsPersonobjectClass: nsAccountobjectClass: nsOrgPersonobjectClass: posixAccountcn: ravidisplayName: Ravi Kumaruid: 12uidNumber: 12gidNumber: 10homeDirectory: /home/ldapuserPassword:: e1BCS0RGMi1TSEE1MTJ9MTAwMDAkQW5qMjcwOUNUTUkyM05vMnFHQnJVNnVCQkE 3Tlk3b3YkcVEvek4xZkVZU0FSTE1mTXV2Nlk5VkNKRmhVMEdxVUlqNXhWdWYxTnZNSmdOMDZ4M3Av QTRhRlRKWDM5TlEySUJQUWNEb2ZuSVlKYm9ESEduZ1JEWGc9PQ==\# search resultsearch: 2result: 0 Success\# numResponses: 6\# numEntries: 5 |
| :---- |

#### Step 7: create user {#step-7:-create-user}

| nano ravi.ldif |
| :---- |

Enter the required details of the user in this file.

Output:

| dn: cn=ravi,ou=users,dc=example,dc=comobjectClass: topobjectClass: nsPersonobjectClass: nsAccountobjectClass: nsOrgPersonobjectClass: posixAccountcn: ravidisplayName: Ravi Kumaruid: 12uidNumber: 12userpassword: 123456gidNumber: 10homeDirectory: /home/ldap |
| :---- |

#### Step 8: add the user in the ldap server {#step-8:-add-the-user-in-the-ldap-server}

| ldapadd \-x \-H ldap://localhost \-D "cn=Directory Manager" \-w Redhat@123 \-f ravi.ldif |
| :---- |

Output:

| adding new entry "cn=ravi,ou=users,dc=example,dc=com" |
| :---- |

Note : to delete a user 

| ldapdelete \-x \-H ldap://localhost \-D "cn=Directory Manager" \-w Redhat@123 "cn=ravi,ou=users,dc=example,dc=com" |
| :---- |

This command will delete the ravi.ldif file containing the user common name ravi that is “cn=ravi”.

#### Step 9: create UI for ldap( install cockpit) {#step-9:-create-ui-for-ldap(-install-cockpit)}

| sudo apt install \-y cockpit |
| :---- |

#### Step 10: start cockpit {#step-10:-start-cockpit}

| sudo systemctl enable \--now cockpit.socket |
| :---- |

#### Step 11: verify the cockpit running  {#step-11:-verify-the-cockpit-running}

| sudo systemctl status cockpit.socket |
| :---- |

Output:

| ● cockpit.socket \- Cockpit Web Service Socket 	Loaded: loaded (/usr/lib/systemd/system/cockpit.socket; enabled; preset: enabled) 	Active: active (running) since Sun 2025-03-23 23:33:00 IST; 2 days ago   Triggers: ● cockpit.service   	Docs: man:cockpit-ws(8) 	Listen: \[::\]:9090 (Stream)  	Tasks: 0 (limit: 8969\) 	Memory: 192.0K (peak: 4.5M)    	CPU: 26ms 	CGroup: /system.slice/cockpit.socketMar 23 23:33:00 pradeep-HP-Laptop-14s-dq5xxx systemd\[1\]: Starting cockpit.socket \- Cockpit Web Service Socket...Mar 23 23:33:00 pradeep-HP-Laptop-14s-dq5xxx systemd\[1\]: Listening on cockpit.socket \- Cockpit Web Service Socket. |
| :---- |

#### Step 11: Access cockpit {#step-11:-access-cockpit}

| xdg-open http://localhost:9090 |
| :---- |

