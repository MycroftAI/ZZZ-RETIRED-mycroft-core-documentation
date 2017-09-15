---
title: 'Configuration'
taxonomy:
    category:
        - docs
---
Mycroft configuration consists of 3 possible config files.
- `mycroft-core/mycroft/configuration/mycroft.conf`, which lives inside the mycroft codebase/distribution
- `/etc/mycroft/mycroft.conf`
- `$HOME/.mycroft/mycroft.conf` (for a package install, $HOME is `/home/mycroft/` as the services are run as the mycroft user)

When the configuration loader starts, it looks in those locations in that order, and loads ALL configuration. Keys that exist in multiple config files will be overridden by the last file to contain that config value.


Skills access these values through the `self.config.get()` function. Use caution when modifying the .conf files.

