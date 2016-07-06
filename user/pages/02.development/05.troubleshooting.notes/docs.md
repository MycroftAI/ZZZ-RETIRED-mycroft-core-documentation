---
title: 'Troubleshooting'
taxonomy:
    category:
        - docs
---
# FAQ/Common Errors
#### Common errors
As errors arise they will be added to the sub-sections below. This will be a good place to start if you encounter a problem when installing and running mycroft-core prior to reaching out to the forum or Slack channels. 

If your questions and issues aren't addressed here please reach out to us via the support channels.

#### When running mycroft, I get the error `mycroft.messagebus.client.ws - ERROR - Exception("Uncaught 'error' event.",)`

This means that you are not running the `./start.sh service` process. In order to fully run Mycroft, you must run `./start.sh service`, `./start.sh skills`, and `./start.sh voice`/`./start.sh cli` all at the same time. This can be done using different terminal windows, or by using the included `./mycroft.sh start`, which runs all three process using `screen`.

