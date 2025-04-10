#     **TEST CASES \- LDAP server setup**

 

| Submitted By | Pradeep Singh |
| :---- | :---- |
| Submitted To | Vipin Tripathi |
| Test Case Version | 1 |
| Reviewer  Name | Moumita Roy |

**Goal :**  To set up an LDAP server inside a Podman container on a Linux system, configure user management using an LDIF file, perform user operations (add, delete, search), and integrate it with an Apache web server to create a UI that displays user details.

       Test Environment : 

* OS: Linux (Ubuntu)  
* LDAP Server: 389 Directory Server  
* Web Server: Apache   
* UI: Cockpit


**Table of Contents**

**[TC1: Installation of 389 Directory Server	2](#tc1:-installation-of-389-directory-server)**

[**TC2: Setting up 389 Directory Server Instance	3**](#tc2:-setting-up-389-directory-server-instance)

[**TC3: Configuring Base DN and Organizational Units	4**](#tc3:-configuring-base-dn-and-organizational-units)

[**TC4:  Creating and Managing Users via LDIF	5**](#tc4:-creating-and-managing-users-via-ldif)

[**TC5:  LDAP User Operations (Add, Delete, Search)	5**](#tc5:-ldap-user-operations-\(add,-delete,-search\))

[**TC6: Install Cockpit	6**](#tc6:-install-cockpit)

[**TC7: Enable and Start Cockpit Service	6**](#tc7:-enable-and-start-cockpit-service)

[**TC8: Verify Cockpit is Running	7**](#tc8:-verify-cockpit-is-running)

[**TC9: Access Cockpit in Browser	8**](#tc9:-access-cockpit-in-browser)

[**TC10: UI for User Search and Display	8**](#tc10:-ui-for-user-search-and-display)

[**TC11: LDAP CRUD operations in UI	9**](#tc11:-ldap-crud-operations-in-ui)


## 


## 

## **TC1:** **Installation of 389 Directory Server** 

| Scenario |  | Install the LDAP server. |  |  |  |
| :---- | ----- | :---- | :---- | :---- | :---- |
| **Remarks:**  |  | Installation is a prerequisite for all other operations; successful installation confirms proper setup of required dependencies. |  |  |  |
| **Given** |  | The system is a Linux machine with package manager access. |  |  |  |
| **When** |  | the administrator installs 389 Directory Server using the package manager |  |  |  |
| **Then** |  | The installation should complete successfully and the version should be displayed when checked.  |  |  |  |
| **Test Run** |  | **Date** |  | **Result** |  |
| Testing outputs  (paste your output/snapshots here ) |  |  |  |  |  |

## **TC2:** **Setting up 389 Directory Server Instance** 

| Scenario |  | Configure and initialize an LDAP instance. |  |  |  |
| :---- | ----- | :---- | :---- | :---- | :---- |
| **Remarks:**  |  | A running LDAP instance ensures the directory service is operational for further configurations. |  |  |  |
| **Given** |  | 389 Directory Server is installed. |  |  |  |
| **When** |  | the administrator creates a new instance interactively and starts the directory service. |  |  |  |
| **Then** |  | the instance should be created and the service should be running. |  |  |  |
| **Test Run** |  | **Date** |  | **Result** |  |
| Testing outputs  (paste your output/snapshots here ) |  |  |  |  |  |

### 

## **TC3: Configuring Base DN and Organizational Units** 

| Scenario |  | Define a directory structure within LDAP. |  |  |  |
| :---- | ----- | :---- | :---- | :---- | :---- |
| **Remarks:**  |  | Setting up the correct hierarchical structure ensures proper organization and access management of LDAP data. |  |  |  |
| **Given** |  | a new LDAP instance is running. |  |  |  |
| **When** |  | The administrator configures a Base DN (e.g., `dc=example,dc=com`) and adds organizational units (e.g., `ou=Users,dc=example,dc=com`). |  |  |  |
| **Then** |  | The directory structure should be successfully created. |  |  |  |
| **Test Run** |  | **Date** |  | **Result** |  |
| Testing outputs  (paste your output/snapshots here ) |  |  |  |  |  |

## 

## **TC4:  Creating and Managing Users via LDIF** 

| Scenario |  | Add user entries using LDIF file |  |  |  |
| :---- | ----- | :---- | :---- | :---- | :---- |
| **Remarks:**  |  | Using LDIF files ensures efficient batch processing of user accounts. |  |  |  |
| **Given** |  | The directory structure is configured. |  |  |  |
| **When** |  | The administrator creates an LDIF file and applies it using `ldapadd`. |  |  |  |
| **Then** |  | Users should be added successfully to the directory. |  |  |  |
| **Test Run** |  | **Date** |  | **Result** |  |
| Testing outputs  (paste your output/snapshots here ) |  |  |  |  |  |

### 

### 

## **TC5:  LDAP User Operations (Add, Delete, Search)** 

| Scenario |  | Perform CRUD operations on LDAP users. |  |  |  |
| :---- | ----- | :---- | :---- | :---- | :---- |
| **Remarks:**  |  | Ensures that LDAP supports user lifecycle management correctly. |  |  |  |
| **Given** |  | LDAP users are present in the directory. |  |  |  |
| **When** |  | The administrator runs `ldapsearch`, `ldapadd`, and `ldapdelete` commands. |  |  |  |
| **Then** |  | The respective operations should execute successfully. |  |  |  |
| **Test Run** |  | **Date** |  | **Result** |  |
| Testing outputs  (paste your output/snapshots here ) |  |  |  |  |  |

## **TC6: Install Cockpit** 

| Scenario |  | Installing Cockpit on Ubuntu system using APT package manager |  |  |  |
| :---- | ----- | :---- | :---- | :---- | :---- |
| **Remarks:**  |  | Ensures Cockpit package is available and can be installed |  |  |  |
| **Given** |  | User has sudo access and internet connection is active |  |  |  |
| **When** |  | The command `sudo apt install -y cockpit`  |  |  |  |
| **Then** |  | Cockpit should install successfully without errors. |  |  |  |
| **Test Run** |  | **Date** |  | **Result** |  |
| Testing outputs  (paste your output/snapshots here ) |  |  |  |  |  |

## **TC7: Enable and Start Cockpit Service** 

| Scenario |  | Enabling and starting Cockpit web service using systemd |  |  |  |
| :---- | ----- | :---- | :---- | :---- | :---- |
| **Remarks:**  |  | Ensures cockpit service starts automatically on boot and starts immediately |  |  |  |
| **Given** |  | Cockpit is installed |  |  |  |
| **When** |  | The command `sudo systemctl enable --now cockpit.socket` is run |  |  |  |
| **Then** |  | The cockpit socket service should be active and running |  |  |  |
| **Test Run** |  | **Date** |  | **Result** |  |
| Testing outputs  (paste your output/snapshots here ) |  |  |  |  |  |

## 

## **TC8: Verify Cockpit is Running**

| Scenario |  | Checking the status of Cockpit web service socket |  |  |  |
| :---- | ----- | :---- | :---- | :---- | :---- |
| **Remarks:**  |  | Confirms that the socket is loaded and actively listening |  |  |  |
| **Given** |  | Cockpit service is enabled and started |  |  |  |
| **When** |  | The command `sudo systemctl status cockpit.socket` is run |  |  |  |
| **Then** |  | Output should show `Active: active (running)` and port `9090` should be listed |  |  |  |
| **Test Run** |  | **Date** |  | **Result** |  |
| Testing outputs  (paste your output/snapshots here ) |  |  |  |  |  |

## **TC9: Access Cockpit in Browser** 

| Scenario |  | Accessing Cockpit Web UI using default port (9090) |  |  |  |
| :---- | ----- | :---- | :---- | :---- | :---- |
| **Remarks:**  |  | Ensures that cockpit web interface is reachable via browser. |  |  |  |
| **Given** |  | Cockpit service is running and port 9090 is open. |  |  |  |
| **When** |  | The command `xdg-open http://localhost:9090` is run or the browser opens manually. |  |  |  |
| **Then** |  | Cockpit login page should load in the browser. |  |  |  |
| **Test Run** |  | **Date** |  | **Result** |  |
| Testing outputs  (paste your output/snapshots here ) |  |  |  |  |  |

## 

## 

## **TC10: UI for User Search and Display** 

| Scenario |  | Create a web UI to fetch and display LDAP user details. |  |  |  |
| :---- | ----- | :---- | :---- | :---- | :---- |
| **Remarks:**  |  | Provides an interactive way for users to query and retrieve LDAP directory data. |  |  |  |
| **Given** |  | LDAP is running and cockpit is configured. |  |  |  |
| **When** |  | A user clicks on a username. |  |  |  |
| **Then** |  | The UI should retrieve and display user details from LDAP. |  |  |  |
| **Test Run** |  | **Date** |  | **Result** |  |
| Testing outputs  (paste your output/snapshots here ) |  |  |  |  |  |

## 

## **TC11: LDAP CRUD operations in UI**

| Scenario |  | Verify LDAP users present in the LDAP. |  |  |  |
| :---- | ----- | :---- | :---- | :---- | :---- |
| **Remarks:**  |  | Ensures that CRUD operations work properly. |  |  |  |
| **Given** |  | Users exist in LDAP. |  |  |  |
| **When** |  |  Try to add,edit and delete a user. |  |  |  |
| **Then** |  | CRUD operation will succeed and show the change when refreshed. |  |  |  |
| **Test Run** |  | **Date** |  | **Result** |  |
| Testing outputs  (paste your output/snapshots here ) |  |  |  |  |  |

## 

## 

## 

## 