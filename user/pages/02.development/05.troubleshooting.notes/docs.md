---
title: 'FAQ and Common Errors'
taxonomy:
    category:
        - docs
---
## FAQ

### How do I change what Mycroft responds to?

To begin, open up your config file or create one in the appropriate user directory (`~/.mycroft/mycroft.ini` is suggested). In there add a new block of config shown below, provided that it doesn't already exist:

```ini
[listener]
wake_word = "hey mycroft"
phonemes = "HH EY . M AY K R AO F T"
threshold = "1e-90"
```

As you may guess, you can replace the "hey mycroft" above with whatever wake word you would like. Along with that you must change the "phonemes" (aka the pronunciation) to this new wake word. To do this you can search for your word or similar ones using [this cmu sphinx English dictionary][cmudict]. If there is a space in the phrase place a period between the words in the phonemes, as demonstrated above.

The last thing to do is to test it out and adjust the threshold value. Decreasing this value (ie. from `1e-90` to `1e-100`) will increase the sensitivity. Going in the opposite direction will make it harder to trigger yet reduce the number of false positives. You will find that this value normally has to be changed a fair amount for every wake word as some require values as high as `1e-10` whereas others need values such as `1e-120` to work.

[cmudict]:http://www.speech.cs.cmu.edu/cgi-bin/cmudict

## Common errors
As errors arise they will be added to the sub-sections below. This will be a good place to start if you encounter a problem when installing and running mycroft-core prior to reaching out to the forum or Slack channels. 

If your questions and issues aren't addressed here please reach out to us via the support channels.

### When running Mycroft, I get the error `mycroft.messagebus.client.ws - ERROR - Exception("Uncaught 'error' event.",)`

This means that you are not running the `./start.sh service` process. In order to fully run Mycroft, you must run `./start.sh service`, `./start.sh skills`, and `./start.sh voice`/`./start.sh cli` all at the same time. This can be done using different terminal windows, or by using the included `./mycroft.sh start`, which runs all three process using `screen`.

### When running Mycroft, I get the error `./start.sh: line 25: /root/.virtualenvs/mycroft/bin/activate: No such file or directory`

The Mycroft virtual environment has not been installed properly. Try running `dev_setup.sh` to make sure that it properly completes.

