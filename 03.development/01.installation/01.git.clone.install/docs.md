---
title: 'Git Clone Install'
taxonomy:
    category:
        - docs
---

## Downloading Mycroft Core

Once you have your development environment set up, you need to download the latest version of `mycroft-core` from github.
To do this, you can either directly download it from our [github page](https://github.com/MycroftAI/mycroft-core) or, if you already know how to use git, you can clone it using `git clone https://github.com/MycroftAI/mycroft-core.git`.

## Creating a Development Environment in Ubuntu/Debian/Fedora/Arch
 - Get into the mycroft-core folder you downloaded using `cd mycroft-core`
 - run `./dev_setup.sh` (feel free to read it)

## Starting in other environments

The following packages are required for setting up the development environment,
 and are what is installed by `dev_setup.sh`, prior to the pip requirements.

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

 The following will set up the development environment on Fedora 25:

```shell
sudo dnf install python python-setuptools python-virtualenv python-gobject \
  python-virtualenvwrapper libtool libffi-devel openssl-devel autoconf bison \
  swig glib2-devel s3cmd portaudio-devel mpg123 libicu-devel
```

After installing the necessary packages, make sure to run the `dev_setup.sh` script that is provided in the `mycroft-core` folder.
