# How to share raster data

## Step 1 - Installing GDAL Binary package

```
$ sudo apt update
$ sudo apt install gdal-bin
```

### Step 2 - Upload an orthomosaic image using SFTP

First create a directory under the DocumentRoot.

```
$ cd /var/www/html
$ sudo mkdir raster_example
$ sudo chown ubuntu:ubuntu raster_example
```

Download an example orthomosaic data for this tutorial.

```
$ wget https://hub.digitalforestry.org/outbox/ppac_rgb_orthomosaic_example.tif
```

Upload it to the server using SFTP. You will need to use a SFTP client for this. I will use FileZilla for the demonstration.

```
Protocol: SFTP
Host: Public IP address
Logon type: Key file
User: ubuntu
Key file: Select the key file you downloaded when creating the instance
```

Now you can upload the downloaded orthomosaic file to the server. You can upload it to the new directory you created above. 

Now collect information about the orthomosaic image you just uploaded. 

```
$ gdalinfo ppac_rgb_orthomosaic_example.tif
```

Information to check

```
EPSG: 32616
Pixel size: 0.01 m
```

Based on the pixel size, we will need to determine what zoom level to use when generating tile maps.

https://wiki.openstreetmap.org/wiki/Zoom_levels

https://docs.mapbox.com/help/glossary/zoom-level/

Since the orthomosaic image has 1 cm GSD, maximum zoom level of 22 would be good enough.

Now you need to create tile maps using *gdal2tiles.py* program

```
$ gdal2tiles.py -z 15-22 -s EPSG:32616 ppac_rgb_orthomosaic_example.tif ppac_rgb
$ gdal2tiles.py -z 15-22 -s EPSG:32616 --xyz ppac_rgb_orthomosaic_example.tif ppac_rgb_xyz
```

Now create a new html file using the template provided [here](https://github.com/gdslab/uas_data_sharing_via_clouds/blob/main/02-share_raster_data/leaflet_template.html)

* You will need to change several things from the template to meet your configurations. 

Once you're done with the edit, then you should be able to visit the html file to visualize the orthomosaic image. 
