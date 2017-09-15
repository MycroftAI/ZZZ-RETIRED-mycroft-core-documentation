---
title: 'Raspberry Pi Install'
taxonomy:
    category:
        - docs
---

##Guide for Getting Started with Picroft, or Mycroft running on a Raspberry Pi!

##Hardware needed for this process:
- Raspberry Pi 3
- At least 8GB Micro SD Card (the image size is right at 4GB, but we recommend extra space to add more skills)
- Wired Speakers plugged into the Audio Out 3.5mm jack on the Raspberry Pi
- USB Microphone (see [the Git Wiki for hardware specifics](https://github.com/MycroftAI/enclosure-picroft/wiki/Hardware))
- Another device with WiFi connection (Computer, Tablet, or SmartPhone)
- USB Keyboard & HDMI Compliant Monitor (Optional but recommended for initial setup)

##Step 1: Download the image file
Check out our blog post and grab the latest .img file:
- [Picroft Download Announcement](https://mycroft.ai/mycroft-now-available-raspberry-pi-image/)

Or download directly from here:
- [Download](https://rebrand.ly/Picroft-0_8)

Then unzip it.


##Step 2: Write it to an SD card
There are instructions on blog post above for Windows, but if you’re using another operating system, check out these guides on Raspberry Pi’s site:

- [Linux](https://www.raspberrypi.org/documentation/installation/installing-images/linux.md)
- [Mac OSX](https://www.raspberrypi.org/documentation/installation/installing-images/mac.md)
- [Windows](https://www.raspberrypi.org/documentation/installation/installing-images/windows.md) (Note: Win32 Disk Imager works fine, but we recommend dotNet Disk Imager)

Just make sure to use the correct image name for the file you downloaded in Step 1:
For example, the linux command to write to an SD card would be:
```
sudo dd bs=4M if=PiCroft_v0.8b_Raspian_JessieLite_2017-01-26.img of=/(PATH OF YOUR SD CARD)



```
##Step 3: Insert in Raspberry Pi and boot it up
Once your image is written, go ahead and pop it out and insert it in the correct slot on the Raspberry Pi. If you aren't wired to the internet, you should get audible prompts to connect to the internet.

##Step 4: Follow the prompts to connect your Picroft to a Wireless Network 
Once your Picroft boots, you need to connect it to the Internet. We would recommend a monitor and keyboard for this, but it’s not absolutely necessary. To get Mycroft onto a wireless network, you’re going to want to connect another device to the MYCROFT network. The password is MYCROFT1. From here, follow the prompts on screen to get your Picroft connected to a Wireless Network of your choice. 



If you haven’t registered this device yet, you’ll do that as well once you’re connected. For that, listen to your code spoken by Picroft (and on screen) and head to home.mycroft.ai to register.


If you haven’t created an account, you’ll be asked to do so. Use whichever method you prefer. 


That's it!

For other resources, such as manual configuration of WiFi, specific hardware tested, and important file locations, check out our wiki on Github:

[Picroft Enclosure Wiki](https://github.com/MycroftAI/enclosure-picroft/wiki)

