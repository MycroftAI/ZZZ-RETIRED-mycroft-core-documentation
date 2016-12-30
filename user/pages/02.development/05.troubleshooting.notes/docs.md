---
title: 'FAQ and Common Errors'
taxonomy:
    category:
        - docs
---
## FAQ

### How do I change what Mycroft responds to?

Visit [Home](https://home.mycroft.ai), log in to your account, and go to the **Settings** page.  Under the Advanced settings you will find the **Listener** section.  In that section is a field labeled **Phonemes**.

Phonemes are basic units of sound, and the value in this field is the wake word Mycroft listens for all the time.  The default value is `HH EY . M AY K R AO F T`, which is how you spell "Hey Mycroft" phonetically.  To figure out the phonetic spelling of a different phrase, you can search for your word or similar ones using this [online CMU Sphinx English dictionary][cmudict]. If there is a space in the phrase place a period between the words in the phonemes, as demonstrated between "EY" and "M" in the default wake word.

The last thing to do is to test it out and adjust the threshold value. Decreasing this value (ie. from `1e-90` to `1e-100`) will increase the sensitivity. Going in the opposite direction will make it harder to trigger yet reduce the number of false positives. You will find that this value normally has to be changed a fair amount for every wake word as some require values as high as `1e-10` whereas others need values such as `1e-120` to work.

[cmudict]:http://www.speech.cs.cmu.edu/cgi-bin/cmudict

## Common errors
As errors arise they will be added to the sub-sections below. This will be a good place to start if you encounter a problem when installing and running mycroft-core prior to reaching out to the forum or Slack channels. 

If your questions and issues aren't addressed here please reach out to us via the support channels.

### When running Mycroft, I get the error `mycroft.messagebus.client.ws - ERROR - Exception("Uncaught 'error' event.",)`

This means that you are not running the `./start.sh service` process. In order to fully run Mycroft, you must run `./start.sh service`, `./start.sh skills`, and `./start.sh voice`/`./start.sh cli` all at the same time. This can be done using different terminal windows, or by using the included `./mycroft.sh start`, which runs all three process using `screen`.

### When running Mycroft, I get the error `./start.sh: line 25: /root/.virtualenvs/mycroft/bin/activate: No such file or directory`

The Mycroft virtual environment has not been installed properly. Try running `dev_setup.sh` to make sure that it properly completes.

