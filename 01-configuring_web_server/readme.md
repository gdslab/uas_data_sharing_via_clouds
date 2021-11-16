# Configuring a web server



## 3. Web server installation Create an Ubuntu Instance on Oracle Cloud Infrastructure (OCI)

## Implementation Procedure

### 1. Introduction

#### 1.1 Purpose
The purpose of this document is to provide information on how to create an Ubuntu instance on **OCI**.
   
#### 1.2 System Overview
The Oracle Cloud Infrastructure (OCI) is is a cloud computing service offered by Oracle Corporation. This service provides a platform where instances can be created. These instances will serve the purpose of hosting our tools for the Unmanned Aerial Vehicle (UAV) online platform.
  
##### 1.2.1 System Description
The system is intended to support hosting and managment of the UAV online platform.

##### 1.2.2 Assumptions and Constraints
Before proceeding please verify the following requirements:
 * Have an OCI account with permission to create instances
 **Have access to a Mac Terminal with internet connection**

##### 1.2.3 System Organization
The system consists of a cloud based server that can be modified to meet your compute and application requirements.

#### 1.3 Glossary
 * **Database:** a structured set of data held in a computer.
 * **HTML:** standard markup language for creating Web pages.
 * **HUB:** connection point in a computer device where data from many directions converge.
 * **MySQL:** open-source relational database management system (RDBMS).
 * **OCI:** cloud computing service offered by Oracle Corporation.
 * **PHP:** server-side scripting language that is embedded in HTML.
 * **Server:** a computer or computer program which manages access to a centralized resource or service in a network.
 * **Terminal:** program, or emulator, which provides a text-based interface for typing commands.
 * **availability domain:** one or more data centers located within a region.
 * **Image:** determines instance's operating system and other software.
 * **Shape:** a resource profile that specifies the number of OCPUs and the amount of memory to be allocated to an instance.

### 2. Management Overview
The implementation required will be provided below as a list of steps to follow. The major tasks involved are:
* Creating an Instance
* Connecting to the Instance
**Setting up a new domain name and add a new TLS certificate**
#### 2.1 Description of Implementation
The system will be implemented using a phased approach. Below is a description of the major tasks:
* Creating an Instance
    * Configure instance resources, select operating system, and save generated SSH key pair.
* Connecting to the Instance
    * Use generated SSH key pair to connect to the instance from the **Mac Terminal**.
**Setting up a new domain name and add a new TLS certificate**
   * Set up a new domain configuration and add a new TLS certificate.  
#### 2.2 Points-of-Contact
Role | Name | Contact
---- | ---- | ----- 
Project/Program Manager | Dr. Jinha Jung | (765) 496-1267
System Developer | Jose Luis Landivar | (817) 704-9757

#### 2.3 Major Tasks
   
1. Creating an Instance
    1. Log in into [Oracle Cloud Infrastructure](https://cloud.oracle.com/)
    2. Select the Menu button > Compute > Instances > Select a compartment > Create instance
    3. Set a name for the instance
    4. On the 'Image and shape' box, click on 'Change image'
    5. From the 'Image source' dropdown, select 'Platform images' > Canonical Ubuntu > click on 'Select image'
    6. Click on 'Change shape' > **select desired shape** > click on 'Select shape'
    7. Scroll down to the 'Add SSH keys' box > click on 'Save Private Key'
    8. Near the bottom of the page, click on 'Create'
    9. Save the 'Public IP address' that has been assigned to the instance
    
2. Connecting to the Instance
    1. Open a terminal window on the folder where the private key is
    2. Type “sudo chmod 600 name.key", where 'name' is the name of the key saved, enter the computer password and press enter
    3. Type “ssh -i name.key ubuntu@address”, where 'name' is the name of the key saved and 'address' is the public ip address assigned, and press enter
    4. Type “yes" and press enter
    5. You are now cconnected to the instance.
        


## 3. Web server installation
### Step 1 - Installing Apache

```
$ sudo apt update
```

```
$ sudo apt install apache2
```

### Step 2 - Adjusting the firewall (OCI)

1. Click the name of the instance you created from the "Compute - Instances" menu.
2. Click "Virtual cloud network" link
3. Click the name of subnet
4. Click "Default Security List for ..." 
5. Click "Add Ingress Rules"
6. Source CIDR: 0.0.0.0/0
7. IP Protocol: TCP
8. Source port range: All
9. Destination port range: 80
10. Description: Web server


### Step 3 - Checking the web server

```
$ sudo systemctl status apache2
```

If this gives you a message *active (running)*, then now you can check the web server through your public IP address

```
http://your_server_ip
```

### Step 4 - DocumentRoot

The **DocumentRoot** is the top-level directory in the document tree visible from the web and this directive sets the directory in the configuration from which the web server looks for and serves web files from the requested URL to the document root. Default **DocumentRoot** is */var/www/html*. 
This means some accesses to *http://your_ip_address/index.html* refers to */var/www/html/index.html*. 
