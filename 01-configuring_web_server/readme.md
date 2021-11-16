# Configuring a web server



## 2. Creating a new instance with Linux OS   
### Step 1 - Creating an Instance
    1. Log in into [Oracle Cloud Infrastructure](https://cloud.oracle.com/)
    2. Select the Menu button > Compute > Instances > Select a compartment > Create instance
    3. Set a name for the instance
    4. On the 'Image and shape' box, click on 'Change image'
    5. From the 'Image source' dropdown, select 'Platform images' > Canonical Ubuntu > click on 'Select image'
    6. Click on 'Change shape' > **select desired shape > click on 'Select shape'
    7. Scroll down to the 'Add SSH keys' box > click on 'Save Private Key'
    8. Near the bottom of the page, click on 'Create'
    9. Save the 'Public IP address' that has been assigned to the instance
    
### Step 2 - Connecting to the Instance
    1. Open a terminal window on the folder where the private key is
    2. Type “sudo chmod 600 name.key", where 'name' is the name of the key saved, enter the computer password and press enter
    3. Type “ssh -i name.key ubuntu@address”, where 'name' is the name of the key saved and 'address' is the public ip address assigned, and press enter
    4. Type “yes" and press enter
    5. You are now connected to the instance.
        


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
