---
title: 'KDE Widget Install'
taxonomy:
    category:
        - docs
---


Note: This feature is still under development, so these instructions might change. 

##Installing Mycroft and the Plasmoid on KDE Neon
The Plasmoid is built on some of the latest technologies, so you need to be running KDE Plasma Desktop 5.9 or later.  If you aren’t using that yet, you can try it out easily using a VM.  Head over to the KDE Downloads page to get an ISO.  You can use that to either create and old-school installer CD, or you can create a VM and load the ISO directly into the virtual disc drive.
Once you have KDE, you can simply download this script and run it.  Here is a step by step:
Go to the Konsole (KDE’s terminal)
- `  cd ~`
- `   wget https://mycroft.ai/to/install_plasmoid_kde.sh `
- `   bash install_plasmoid_kde.sh `
That’s it!  You’ll be prompted a couple times to enter a password and the compile process will take a while, but it is straightforward.

##Installing Mycroft and the Plasmoid on Fedora KDE
Fedora KDE users can try this too.  All you need to do is go to the Terminal and type the following commands:
- `cd ~ `
- `   wget https://mycroft.ai/to/install_plasmoid_fedora.sh `
- `   bash install_plasmoid_fedora.sh `

##Adding it to your Desktop
After the install completes right click on the desktop and select “Add Widget…”.  Scroll through the list until you see “Project Mycroft”, then just click and drag it to your desktop.