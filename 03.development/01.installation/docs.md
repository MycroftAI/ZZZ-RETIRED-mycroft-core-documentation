---
title: 'Getting Started'
taxonomy:
    category:
        - docs
---
# Setting up Mycroft

Currently, Mycroft only runs in Linux environments. If you already have a Linux desktop environment, you can go ahead and skip to the appropriate install section:

[Git-Clone](https://docs.mycroft.ai/installing.and.running/installation/git.clone.install)  
[Raspberry Pi](https://docs.mycroft.ai/installing.and.running/installation/raspberry.pi)   
[Package Install](https://docs.mycroft.ai/installing.and.running/installation/apt-get.install)    
[Docker Image](https://docs.mycroft.ai/installing.and.running/installation/docker.install)   


## Setting Up Mycroft on non-Linux Operating Systems
For those who use MacOS or Windows, you can use something like [VirtualBox](https://www.virtualbox.org/wiki/Downloads) to set up a virtual Linux environment. To do this:
 - Install VirtualBox or another similar piece of software
 - Download an image of your preferred distribution of Linux from something like [osboxes.org](http://www.osboxes.org/). If you're not sure about distributions, we recommend using Ubuntu 16.04 as that is what our current setup scripts are targeted at.
 - Import your image into VirtualBox
 - Make sure you allocate at least 15 GB of hard drive space, 3 GB of Ram, and 2 cores of your processor. If you run it with one core, that's fine, but keep in mind it will take Mimic a long time to build. 
 
 From there, go to the [git clone install](https://docs.mycroft.ai/installing.and.running/installation/git.clone.install)


