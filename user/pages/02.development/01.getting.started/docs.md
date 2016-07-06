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
 - Download an image of your preferred distribution of Linux from something like [osboxes.org](osboxes.org). If you're not sure about distributions, we recommend using Ubuntu 16.04, as that is what our current setup scripts are targeted at.
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

# Getting set up using Docker
- <i>WIP: More information coming soon.</i>
