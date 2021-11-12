# How to share raster data


## Step 1 - Installing Apache

```
$ sudo apt update
```

```
$ sudo apt install apache2
```

## Step 2 - Adjusting the firewall

```
$ sudo ufw app list
```

```
$ sudo ufw allow 'Apache'
```

```
$ sudo ufw status
```


## Step 3 - Checking the web server

```
$ sudo systemctl status apache2
```

If this gives you a message *active (running)*, then now you can check the web server through your public IP address

```
http://your_server_ip
```

## Step 4 - DocumentRoot

The **DocumentRoot** is the top-level directory in the document tree visible from the web and this directive sets the directory in the configuration from which the web server looks for and serves web files from the requested URL to the document root. Default **DocumentRoot** is */var/www/html*. 
This means some accesses to *http://your_ip_address/index.html* refers to */var/www/html/index.html*. 
