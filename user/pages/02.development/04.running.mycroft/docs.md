---
title: 'Running Mycroft'
taxonomy:
    category:
        - docs
---

# Running scripts

### Using `mycroft.sh`
Mycroft has a shell script `mycroft.sh` that can be used to run the voice, command line interface, service, and skills processes all at once using screens. To start, just run `./mycroft.sh start` and to kill all processes, run `./mycroft.sh stop`. You can also use `./mycroft.sh start -c` to run just service, skills, and command line or `./mycroft.sh start -v` to run just service, skill, and voice. To see all of the currently running screens, use `screen -list`. To attach one of the screens to see the output, use `screen -r <screen-name>`. For more information about screens, take a look at the [screen manual](https://www.gnu.org/software/screen/manual/screen.html).

### Using `start.sh`
Mycroft also provides the shell script `start.sh` to run a large number of common tasks. This script uses the virtualenv created by
`dev_setup.sh`. The usage statement lists all run targets, but to run a Mycroft stack out of a git checkout, the following processes should be started:
run `./start.sh service`
run `./start.sh skills`
run `./start.sh voice`

*Note: The above scripts are blocking, so amke sure to run each of them in a separate terminal session.*

### Using Virtualenv and Python

Activate your virtualenv.

With virtualenv-wrapper:
```
workon mycroft
```

Without virtualenv-wrapper:
```
source ~/.virtualenvs/mycroft/bin/activate
```
- run `PYTHONPATH=. python client/speech/main.py` # the main speech detection loop, which prints events to stdout and broadcasts them to a message bus
- run `PYTHONPATH=. python client/messagebus/service/main.py` # the main message bus, implemented via web sockets
- run `PYTHONPATH=. python client/skills/main.py` # main skills executable, loads all skills under skills dir

*Note: The above scripts are blocking, so each will need to be run in a separate terminal session. Each terminal session will require that the virtualenv be activated. There are very few reasons to use this method.*

# Interacting with Mycroft

Once you have the processes running in some form, it's very easy to start using Mycroft. Simply say `Hey Mycroft` followed by what you want him to respond to. A simple example is something like `Hey Mycroft, what time is it?`. Take a look at our [skills page](https://docs.mycroft.ai/features) for a more extensive list of what you can ask Mycroft.
