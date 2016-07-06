---
title: 'Audio issues'
taxonomy:
    category:
        - docs
---
# Audio errors and issues
If your questions and issues aren't addressed here please reach out to us via the support channels.

## Alsa
Alsa is the sound architecture on most linux systems, but particularly on Ubuntu and Raspbian. It comes with a series of tools used to select a usb audio device and configure them for use with your device.

Most of the Alsa configuration is done on the command line. Below are some useful links and configuration files to help you setup and debug your system. Note that these are by no means all of the commands you will need. You should still look up configuration files for your own distribution. Alsa changes frequently with new linux distributions and releases, so it's still helpful to Google things.

### Useful audio cli commands and apps

 - aplay -l
    - Command line audio-player, lists audio devices
 - aplay -L
    -  List all PCMs defined
 - lsusb
    - Shows all plugged in usb devices, including your audio device.
    - For example, some audio devices show up as C-media usb
 - pulseaudio -D
    - Puleaudio is a sound application. To install, run  `apt-get install pulseaudio`
    - The -D option runs the daemon, which needs to be running on the device for audio to work
    - The application is run visually. Look in your apps to find it.
 - alsamixer
    - Alsamixer is a built-in [sound mixer](http://www.linuxplanet.com/linuxplanet/tutorials/7134/1) that lets you select your device and get it running from the command line.

### Raspbian and Ubuntu Jessie

Jessie has moved the alsa configuration files. See below for the new files and locations. 

 - General Alsa docs: ![docs](http://alsa.opensrc.org/MultipleCards#alsa.conf_structure)
 - Config files
    - /usr/share/alsa/alsa.conf
    - ~/.asoundrc

#### Mycroft voice Alsa error: `ALSA lib confmisc.c:768:(parse_card) cannot find card '0'` when running ./mycroft.sh start

We see this error on initial install and running the setup for mycroft-core on a raspberry Pi 3 device prior to the Cerberus registration. The error displayed indicates that the Raspbian install had issues finding the usb device and card 0. We saw the [kinobo usb 2.0 device but but could not utilize it.](https://www.amazon.com/Kinobo-Microphone-Desktop-Recognition-Software/dp/B00IR8R7WQ)

The solution for this problem was found in [this](http://raspberrypi.stackexchange.com/questions/37177/best-way-to-setup-usb-mic-as-system-default-on-raspbian-jessie) StackOverflow(SO) post. This worked for the Kinobo device but should help others with different usb devices find their card #s.

Short version of the instructions listed below:

 1. Discover Card and Device # by running lsusb (See below).
 2. Run `sudo nano /usr/share/alsa/alsa.conf`
    1. Change numbers below to your card # (1 for my kinobo build)
    2. `defaults.ctl.card 0` to `defaults.ctl.card yourcard#`
    3. `defaults.pcm.card 0` to `defaults.pcm.card yourcard#`
 4. Create and edit your personal alsa configuration file by running `sudo nano~/.asoundrc` and changing to your card #.

> pcm.!default  {
>     type hw
>     card 1 }
> 
> ctl.!default {
>     type hw
>     card 1 }

 5. Run `sudo reboot`
 6. You may need to run `pulseaudio -D` again prior to running the mycroft start script.
 7. Finally run `./mycroft.sh start` from the instructions. That should now discover the device and you should be able to get your cerberus registration code.

##### Getting your audio device and card #
Get lsusb readout (The C-Media is my usb audio device):

   $ lsusb
      Bus 001 Device 004: ID 0d8c:013c C-Media Electronics, Inc. CM108 Audio Controller
      Bus 001 Device 005: ID 0c40:8000
      Bus 001 Device 003: ID 0424:ec00 Standard Microsystems Corp. SMSC9512/9514 Fast Ethernet Adapter
      Bus 001 Device 002: ID 0424:9514 Standard Microsystems Corp.
      Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

Get a list of your audio cards with:

    $ cat /proc/asound/cards
    1 [Device         ]: USB-Audio - USB PnP Sound Device
                      C-Media Electronics Inc. USB PnP Sound Device at usb-3f980000.usb-1.4, full spe

Knowing the card # you can get the rest of the info by changing card1 to your card:

    $ cat /proc/asound/card1/pcm0c/info
       card: 1
       device: 0
       subdevice: 0
       stream: CAPTURE
       id: USB Audio
       name: USB Audio
       subname: subdevice #0
       class: 0
       subclass: 0
       subdevices_count: 1
       subdevices_avail: 1

### Raspbian and Ubuntu Wheezy

 - Config files
    - /etc/modprobe.d/alsa-base.conf

