---
title: 'Configuration'
taxonomy:
    category:
        - docs
---
Mycroft configuration consists of 3 possible config files.
- `mycroft-core/mycroft/configuration/mycroft.ini`, which lives inside the mycroft codebase/distribution
- `/etc/mycroft/mycroft.ini`
- `$HOME/.mycroft/mycroft.ini`

When the configuration loader starts, it looks in those locations in that order, and loads ALL configuration. Keys that exist in multiple config files will be overridden by the last file to contain that config value. This results in a minimal amount of config being written for a specific device/user, without modifying the distribution files.
