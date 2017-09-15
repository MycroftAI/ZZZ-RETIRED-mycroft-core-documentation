---
title: 'Running and Interacting with Mycroft'
taxonomy:
    category:
        - docs
---
#   Guide to Running Mycroft

## Running scripts (after a git-clone installation method)

### Note:
If this is the first time running Mycroft, you will have to pair before Mycroft can answer questions, for tips on that, check out our [Pairing Guide](https://docs.mycroft.ai/installing.and.running/pairing).

### Using `mycroft.sh`
Mycroft has a shell script `mycroft.sh` that can be used to run the voice, command line interface, service, and skills processes all at once using screens. To start, just run `./mycroft.sh start` and to kill all processes, run `./mycroft.sh stop`. You can also use `./mycroft.sh start -c` to run just service, skills, and command line or `./mycroft.sh start -v` to run just service, skill, and voice. `./mycroft.sh start -d` runs Mycroft in a quiet mode and opens to the CLI screen immediately. 

### Using `start.sh`
Mycroft also provides the shell script `start.sh` to run a large number of common tasks. This script uses the virtualenv created by
`dev_setup.sh`. The usage statement lists all run targets, but to run a Mycroft stack out of a git checkout, the following processes should be started:  
run `./start.sh service`  
run `./start.sh skills`  
run `./start.sh voice`  

You can also run the CLI client via start. 
run './start.sh cli'  or for silent operation  
run './start.sh cli --quiet'  

*Note: The above scripts are blocking, so make sure to run each of them in a separate terminal session.*

### Stopping Mycroft
To stop Mycroft, run 
`./mycroft.sh start`  
You can also stop each individual service by ^c on the correct screen.

If you run mycroft using `./mycroft.sh start`, you can swap to the relevant services using screen commands. For more on that, see below.



##Running Mycroft on the Raspberry Pi
Mycroft starts running immediately when the Pi boots, so there should be nothing you need to do. Check out the interacting with Mycroft below to get using it.


##KDE Method to Starting and Stopping Mycroft
Using the Plasmoid
Click on the Mycroft icon to open it up.  You”ll need to click the ▶️️ button at the top to tell Mycroft to begin listening.  Then you can say “Hey Mycroft, register my device” to create your pairing with home.mycroft.ai.  You’ll immediately notice the text is both spoken and displayed on screen in the widget.
In the alpha there were special handlers for “What’s the weather like?” that began to show the possibilities of combining voice interaction with a screen, combining voice and visuals.  We’ll be exposing those capabilities to our Skill API soon for other developers to explore.

##Running Mycroft after a package install
Just like the Picroft install, the package install runs automatically after a boot. 

# Interacting with Mycroft

Once you have the processes running in some form, it's very easy to start using Mycroft. Simply say `Hey Mycroft` followed by what you want him to respond to. A simple example is something like `Hey Mycroft, what time is it?`. Take a look at our [skills page](https://docs.mycroft.ai/skills.and.features) for a more extensive list of what you can ask Mycroft.

##Screens and other tools
Mycroft uses screens when it runs. This is helpful as you don't need to be watching every screen at once and it allows you to run Mycroft in the background.
There are 4 screens that run when you start up Mycroft:
- CLI -- This is the command line interface. You can use it instead of a microphone and simply type commands.
- Voice -- This is going to be responding to trigger words and what mycroft says. 
- Skills -- Executes the skills. When debugging skills, this will be a major source of information.
- Service -- This is the backend for Mycroft. Unless you're having major problems with Mycroft, this will be less useful. 

To see all of the currently running screens, use `screen -list`. To attach one of the screens to see the output, use `screen -r <screen-name>`. For more information about screens, take a look at the [screen manual](https://www.gnu.org/software/screen/manual/screen.html).



##Command Line tools for the Raspberry Pi
The Raspberry Pi doesn't use screens, just runs everything in the background as you effectively just have 1 terminal window running. To interact with the different elements of Mycroft on the pi, you can run any of the following commands from the command-line.

By default, Picroft boots into the view-log mode. To get back to this at any time, type
- `view_log'

in the terminal. To get out of this, press Control-C.

There are 4 other Mycroft tools you can access from the command line as well. 


###Mycroft Skills Manager
The Mycroft Skills Manager is a work in progress. It does allow you to install new skills hosted on the github Skills repo:

[Mycroft Skills Repository](https://github.com/MycroftAI/mycroft-skills)

You can get information on it through:

- 'msm' 

####Other features of msm:

- 'msm list'

Will list all currently available skills that are hosted on the repo.

- 'msm install $GITHUB PATH OR SKILL NAME'

Allows you to install from the given repo or install a skill by name. Some skills have dependancies that the msm may miss, so make sure to look at github to ensure the skill will work. It effectively clones the skill for you and places it in the correct directory.

###Command Line Client

- 'cli'

###Say
This let's you send a one-shot command to Mycroft by using say:
- 'say $WHAT YOU WANT TO SAY TO MYCROFT'

For example:
- 'say what's the weather'

Activates the weather skill and has Mycroft read you the weather. You are then left back in console.

###Test Microphone

- 'test_microphone'

This let's you record from your microphone for a few seconds and then plays it back. Useful for making sure those two devices work.


