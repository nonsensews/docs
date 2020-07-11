title:  How To Install TorchCraft and Set Up a Programming Environment on Linux
date: 2020-07-09
description: TorchCraft is a BWAPI module that sends StarCraft data out over a ZMQ connection. This lets you parse game data and interact with BWAPI. 

{% img [class name(s)] /images/python.jpg %}

Python is an interpreted, high-level, general-purpose programming language with strengths in automation, data analysis and machine learning.

This tutorial will walk you through installing Python 3 and setting up a programming environment on Debian 10.

## Step 0 - Update and Upgrade

Logged into your system as root, first update and upgrade to ensure your shipped version of Python 3 is up-to-date.

```
apt update
```

```
apt upgrade
```

Confirm upgrade when prompted to do so.


## Step 1 - Check Version of Python

Check your version of Python 3 installed by typing:

```
python3 --version
```

You'll receive output similar to the following.

```
Python 3.7.3
```

## Step 2 - Install pip

To manage software packages for Python, install `pip`, the standard package installer for Python. You can use pip to install things from the official package index and other indexes. 

```
apt install -y python3-pip
```

Python packages can be installed by typing:

```
pip3 install schematics 
```

Here, `schematics` can refer to any Python package, such as tornado for backend development or NumPy for scientific computing. 

## Step 3 - Install Additional Tools

There are a few more packages and development tools to install to ensure that we have a robust set-up for our StarCraft: Brood War Python TorchCraft bots programming environment:

```
apt -y install --install-recommends git apt-transport-https\
 gnupg2 wget software-properties-common curl build-essential\
 gfortran pkg-config make cmake libyaml-0-2 libyaml-dev vim
```

```
dpkg --add-architecture i386
```

```
apt-add-repository contrib 
```

```
apt -y install --install-recommends libgnutls30:i386 libldap-2.4-2:i386\
 libgpg-error0:i386 libxml2:i386 libasound2-plugins:i386 libsdl2-2.0-0:i386\
 libfreetype6:i386 libdbus-1-3:i386 libsqlite3-0:i386 libgl1-mesa-glx:i386\
 libgl1-mesa-dri:i386 libsdl2-2.0-0 libstb0 libstb0:i386 mesa-vulkan-drivers
```

## Step 4 - Add the WineHQ Debian repository

Get and install the repository key.

```
wget -nc https://dl.winehq.org/wine-builds/winehq.key && apt-key add winehq.key
```

```
apt-add-repository 'deb https://dl.winehq.org/wine-builds/debian/ buster main'
```

```
apt update && rm winehq.key
```
## Step 5 - Install libfaudio0 and Wine

As of Wine 4.5+, libfaudio0 is required by the devel and staging packages provided by WineHQ but is not included in the Wine HQ packages, which means you are responsible for making libfaudio0 available prior to installing Wine. This tutorial explains how to obtain libfaudio0 for Debian 10. Distributions which include libfaudio0 in their repository are not subject to this problem.

```
wget -nc https://download.opensuse.org/repositories/Emulators:/Wine:/Debian/Debian_10/amd64/libfaudio0_20.01-0~buster_amd64.deb
```

```
wget -nc https://download.opensuse.org/repositories/Emulators:/Wine:/Debian/Debian_10/i386/libfaudio0_20.01-0~buster_i386.deb
```

```
dpkg -i libfaudio0_20.01-0~buster_amd64.deb
```

```
dpkg -i libfaudio0_20.01-0~buster_i386.deb
```

```
apt -y install --install-recommends winehq-staging winetricks
```

## Step 6 - Configuring WINE

Many programs work under WINE with absolutely no configuration. Unfurtunately, this isn't the case.

### (default) hanlde things using your own session

```
TBD
```


### (optional) handle things using a separate `wine` user
```
adduser --disabled-login --gecos "" --shell /forbid/login wine
```

```
usermod --append --groups audio wine
```

```
chown wine:wine -R /home/wine
```

```
sudo -u wine env HOME=/home/wine USER=wine USERNAME=wine LOGNAME=wine WINEARCH=win32 wineboot
```




## Step 7 - TorchCraft: Brood War 1.16.1

### TorchCraft

TDB

### StarCraft

At the moment StarCraft: Remastered is *NOT* yet supported, the only working version is 1.16.1.

```
git clone https://github.com/spacebeam/starcraft-sif.git /usr/src/starcraft-sif
```

In this tutorial we have StarCraft installed in `/opt/StarCraft/`
```
cat /usr/src/starcraft-sif/include/core/core* > /opt/StarCraft.tar.gz
```

```
tar -zxvf /opt/StarCraft.tar.gz -C /opt/
```

## Step 8 - Coding & Building

Lets create a small Terran bot with a single timing attack. Check out the examples!

### Run your bot
```
TBD
```

### Run Chaoslauncher
```
TBD
```

## Step 9 - Setting up bwapi.ini