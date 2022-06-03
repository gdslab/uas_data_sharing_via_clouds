# Configuring a web server

      
## 3. Web server installation

### Step 1 - Installing Apache

Install apache http

```
$ sudo apt update
$ sudo apt install apache2
```

Createt firewall rules to allow access to the ports on which the HTTP server listens.

```
$ sudo apt install firewalld
$ sudo firewall-cmd --permanent --zone=public --add-service=http
$ sudo firewall-cmd --reload
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

### Step 3 - Checking if the web server is up and running

You can visit http://<public_ip_address> in your browser. You should see the index page of the web server you just created above. 

### Step 4 - DocumentRoot

The **DocumentRoot** is the top-level directory in the document tree visible from the web and this directive sets the directory in the configuration from which the web server looks for and serves web files from the requested URL to the document root. Default **DocumentRoot** is */var/www/html*. 
This means some accesses to *http://your_ip_address/index.html* refers to */var/www/html/index.html*. 
