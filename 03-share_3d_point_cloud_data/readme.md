# How to share 3D point cloud data

## Installing PotreeConverter 2.1

This instruction is designed for Ubuntu 20.04. 

### Configuration for Ubuntu 20.04

```
$ sudo apt install build-essential cmake g++
$ sudo apt install libtbb-dev
```

### Then install lastools

```
$ cd ~/dev/workspaces/lastools
$ git clone https://github.com/m-schuetz/LAStools.git master
$ cd master/LASzip
$ mkdir build
$ cd build
$ cmake -DCMAKE_BUILD_TYPE=Release ..
$ make
```

### Install PotreeConverter

First check out 2.1 version

```
$ cd ~/dev/workspaces/PotreeConverter
$ git clone https://github.com/potree/PotreeConverter.git master
$ cd master
$ git checkout tags/2.1
$ mkdir build
$ cd build
$ cmake -DCMAKE_BUILD_TYPE=Release -DLASZIP_INCLUDE_DIRS=~/dev/workspaces/lastools/master/LASzip/dll -DLASZIP_LIBRARY=~/dev/workspaces/lastools/master/LASzip/build/src/liblaszip.so ..
$ make
```

## Example point cloud data

```
$ wget https://hub.digitalforestry.org/outbox/3d_plant_example.las
```

## Convert las file to Potree format

First make a directory to save converted files.

```
$ mkdir /var/www/html/potree_data
```

Using *PotreeConverter*, now convert the las file into potree format

```
$ cd ~/dev/workspaces/PotreeConverter/master/build
$ ./PotreeConverter /var/www/html_block/data/3d_plant_example.las -o /var/www/html_block/potree_data
```

Now copy *lib* directory to the DOCUMENTROOT

```
$ cd resources/page_template
$ cp -r libs /var/www/html
```

Now Create a new html file using the template 
