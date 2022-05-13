# How to share 3D point cloud data

## Installing PotreeConverter 1.7

Following https://github.com/potree/PotreeConverter/tree/1.7

First, install git

```
$ sudo yum install git
```

Then, install required tools

```
$ sudo yum install libmpc-devel mpfr-devel gmp-devel gcc gcc-c++ git cmake boost-devel
```

Then install lastools

```
$ cd ~/dev/workspaces/lastools
$ git clone https://github.com/m-schuetz/LAStools.git master
$ cd master/LASzip
$ mkdir build
$ cd build
$ cmake -DCMAKE_BUILD_TYPE=Release ..
$ make
```

Install PotreeConverter

```
$ cd ~/dev/workspaces/PotreeConverter
$ wget https://github.com/potree/PotreeConverter/archive/refs/tags/1.7.tar.gz
$ tar xvf 1.7.tar.gz
$ mv PotreeConverter-1.7 master
$ cd master
$ mkdir build
$ cd build
$ cmake -DCMAKE_BUILD_TYPE=Release -DLASZIP_INCLUDE_DIRS=~/dev/workspaces/lastools/master/LASzip/dll -DLASZIP_LIBRARY=~/dev/workspaces/lastools/master/LASzip/build/src/liblaszip.so ..
$ make
```
