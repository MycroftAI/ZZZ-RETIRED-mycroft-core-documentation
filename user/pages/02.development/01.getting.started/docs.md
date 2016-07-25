---
title: 'Getting Started'
taxonomy:
    category:
        - docs
---
# Setting up the development environment

Currently, Mycroft only runs in Linux environments. If you already have a Linux desktop environment, you can go ahead and skip to the `Downloading Mycroft Core` section. 

For those who use MacOS or Windows, you can use something like [VirtualBox](https://www.virtualbox.org/wiki/Downloads) to set up a virtual Linux environment. To do this:
 - Install VirtualBox or another similar piece of software
 - Download an image of your preferred distribution of Linux from something like [osboxes.org](http://www.osboxes.org/). If you're not sure about distributions, we recommend using Ubuntu 16.04, as that is what our current setup scripts are targeted at.
 - Import your image into VirtualBox

## Downloading Mycroft Core

Once you have your development environment set up, you need to download the latest version of `mycroft-core` from github. 
To do this, you can either directly download it from our [github page](https://github.com/MycroftAI/mycroft-core) or, if you already know how to use git, you can clone it using git.

## Starting in Ubuntu - Development Environment
 - Get into the mycroft-core folder that you downloaded using `cd mycroft-core`
 - run `./build_host_setup.sh` (installs debian packages with apt-get, please read it)
 - run `./dev_setup.sh` (feel free to read it, as well)
 
## Starting in other environments

The following packages are required for setting up the development environment,
 and are what is installed by `build_host_setup.sh`

 - `git`
 - `python 2`
 - `python-setuptools`
 - `python-virtualenv`
 - `pygobject`
 - `virtualenvwrapper`
 - `libtool`
 - `libffi`
 - `openssl`
 - `autoconf`
 - `bison`
 - `swig`
 - `glib2.0`
 - `s3cmd`
 - `portaudio19`
 - `mpg123`

 The following packages are required for setting up the development environment on Fedora 23

 - `git`
 - `python 2`
 - `python-setuptools`
 - `python-virtualenv`
 - `pygobject2`
 - `python-virtualenvwrapper`
 - `libtool`
 - `libffi`
 - `openssl`
 - `autoconf`
 - `bison`
 - `swig`
 - `glib2`
 - `s3cmd`
 - `portaudio`
 - `portaudio-devel`
 - `mpg123` (Available in RPMFusion)
 
After installing the necessary packages, make sure to run the `dev_setup.sh` script that is provided in the `mycroft-core` folder. 

# Installing using apt (experimental)
It is currently possible to install mycroft-core on any Debian based system (amd64 and armhf.) For developers, it is recommended to use the git checkout method. It is also possible to attach an interface to the Mycroft messagebus or use the Skills SDK to develop outside of the core. In this case installing with apt may be useful to you.

Currently there are two channels: `debian` and `debian-unstable`. The `debian` repository will track releases, with a schedule of release every thursday. Use this for a stable build. The `debian-unstable` repository builds packages based on master, and is build every night or even more frequently. This is to allow us to confirm that changes made to the core wont break the release packages.

 Enabling TLS for apt
 In order to use a repository with TLS support, it must be enabled.
 - `sudo apt-get install apt-transport-https`


Download and install signing key from keyserver.
 - `sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys F3B1AA8B`


Create apt source entry (stable releases).
 - `sudo echo "deb http://repo.mycroft.ai/repos/apt/debian debian main" > /etc/apt/sources.list.d/repo.mycroft.ai.list`


Alternativly, create apt source entry (unstable, daily master builds or more frequent).
 - `sudo echo "deb http://repo.mycroft.ai/repos/apt/debian debian-unstable main" > /etc/apt/sources.list.d/repo.mycroft.ai.list`

Updating the apt cache to include the new repository
 - `sudo apt-get update`


Installing mycroft-core
 - `sudo apt-get install mycroft-core`


Debian package specific notes:
The following system services will be created in `/etc/init.d/`:
 - `mycroft-messagebus`
 - `mycroft-skills`
 - `mycroft-speech-client`

Mycroft units will include an additional client for faceplate interaction.
 - `mycroft-enclosure-client`


These services can be started and stopped in this manner:
 - `service mycroft-messagebus start`
 - `service mycroft-messagebus stop`


Log files will also be created.
 - `/var/log/mycroft-messagebus`
 - `/var/log/mycroft-skills`
 - `/var/log/mycroft-speech-client`


In addition, a default configuration file will be created in `/etc/mycroft.ini`.

Even though Mycroft services will be controlled by the system, they will be run as the `mycroft` user. Additional configuration as well as the location of the identity.json file will be created in `/home/mycroft/.mycroft/`.

# Getting set up using Docker
- <i>WIP: More information coming soon.</i>
