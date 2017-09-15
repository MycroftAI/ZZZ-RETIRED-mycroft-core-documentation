---
title: 'Package Install'
taxonomy:
    category:
        - docs
---

At this point, this is a still a work in progress and not recommend. We recommend using the Git Install method.

# Installing using apt (experimental)
It is currently possible to install mycroft-core on any Debian based system (amd64 and armhf.) For developers, it is recommended to use the git checkout method. It is also possible to attach an interface to the Mycroft messagebus or use the Skills SDK to develop outside of the core. In this case installing with apt may be useful to you.

Currently there are two channels: `debian` and `debian-unstable`. The `debian` repository will track releases with a schedule of release every Thursday. Use this for a stable build. The `debian-unstable` repository builds packages based on master, and is build every night or even more frequently. This is to allow us to confirm that changes made to the core wont break the release packages.

In order to use a repository with TLS support, it must be enabled.
 - `sudo apt-get install apt-transport-https`

Download and install signing key from keyserver.
 - `sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys F3B1AA8B`

Create apt source entry (stable releases).
 - `sudo bash -c 'echo "deb http://repo.mycroft.ai/repos/apt/debian debian main" > /etc/apt/sources.list.d/repo.mycroft.ai.list'`
 
    **or** for the daily master builds (unstable, more frequent)

   `sudo bash -c 'echo "deb http://repo.mycroft.ai/repos/apt/debian debian-unstable main" > /etc/apt/sources.list.d/repo.mycroft.ai.list'`

Update the apt cache to include the new repository
 - `sudo apt-get update`

Install mycroft-core
 - `sudo apt-get install mycroft-core`

Debian package specific notes:
The following system services will be created in `/etc/init.d/`:
 - `mycroft-messagebus`
 - `mycroft-skills`
 - `mycroft-speech-client`

Mycroft units will include an additional client for faceplate interaction.
 - `mycroft-enclosure-client`

Each service can be started and stopped in this manner:
 - `service mycroft-messagebus start`
 - `service mycroft-messagebus stop`

Log files are created here:
 - `/var/log/mycroft-messagebus.log`
 - `/var/log/mycroft-skills.log`
 - `/var/log/mycroft-speech-client.log`
 - `/var/log/mycroft-enclosure-client.log`

In addition, a default configuration file will be created in `/etc/mycroft/mycroft.conf`.

Even though Mycroft services will be controlled by the system, they will be run as the `mycroft` user. Additional configuration as well as the location of the identity.json file will be created in `/home/mycroft/.mycroft/`.
