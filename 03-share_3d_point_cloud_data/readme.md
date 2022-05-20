# How to share 3D point cloud data

## Installing PotreeConverter 1.7

This instruction is designed for Ubuntu 20.04. 

### Configuration for Ubuntu 20.04

```
$ sudo apt install build-essential cmake g++
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

First check out 1.7 version

```
$ cd ~/dev/workspaces/PotreeConverter
$ git clone https://github.com/potree/PotreeConverter.git master
$ cd master
$ git checkout tags/1.7
```

Then I need to update changes to make compile successful. For this, I need to install Github CLI first.

```
$ curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
$ sudo apt update
$ sudo apt install gh
```

Now, you need to create a token to work with gh. Visit https://github.com/settings/tokens to create a new token.
Make it sure to check **repo** and **read:org**. After this, you will need to log in using 

```
$ gh auth login
```

Then check out the modified version
```
$ gh pr checkout 405
```

Then, finish up the rest of process.

```
$ mkdir build
$ cd build
$ cmake -DCMAKE_BUILD_TYPE=Release -DLASZIP_INCLUDE_DIRS=~/dev/workspaces/lastools/master/LASzip/dll -DLASZIP_LIBRARY=~/dev/workspaces/lastools/master/LASzip/build/src/liblaszip.so ..
$ make
```
