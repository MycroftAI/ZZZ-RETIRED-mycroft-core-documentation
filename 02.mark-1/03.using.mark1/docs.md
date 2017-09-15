---
title: Using Mark 1
taxonomy:
    category:
        - docs
---

# Voice Command List
Currently the below skills are available out of the box, you can find more skills at the
[Mycroft Skill Repo](https://github.com/MycroftAI/mycroft-skills)

- [Register | pair] [this | my] device. (register with home.mycroft.ai)
- What is your IP address? (displays & reads network interface addresses)
- Install [X] skill.
- Who are you?
- What are you?
- Who made you?
- When were you born?
- Where were you born?
- What are you made of?
- Where do you come from?
- What time is it?
- What is today's (tomorrow's) date?
- What is the weather?
- Set a timer for [X] minutes.
- Remind me at [XX:XX] | [in X mins|secs|hours] to do [X].
- [Raise | lower | set to 1-10 | mute] volume.
- Say [X] (repeats phrase)
- Sing a song.
- Spell [X].
- Tell me about [X] (Wikipedia search)
- What / when / where [X]? (Wolfram Alpha search)
- What is the current stock price of [X]?
- Play the news.
- [Start | stop | play] recording.
- Tell me a joke!

# Accessing Mark 1 Menu
Below are the steps to access the menu on the Mark 1 device.  This will let you enable ssh, manually reboot, etc.

1. Hold down the mark 1 button for two seconds to get to the menu.
2. You can toggle between the below options by rotating the button then pushing in on the button once you find your selection.

You can pick from these options on the screen menu:
- ILLUM - change the brightness of the eyes
- WIFI - setup or change wifi
- REBOOT - restart the mark 1
- OFF - turn off the mark 1
- TEST - test my lights, speaker, and mic
- SSH - enable/disable ssh option.
- RESET - wipe the data on the mark 1 and reset to factory default
- EXIT - leave the menu

# Access Mark 1 CLI
You can access the CLI of the mark 1 by running the following command from the CLI, then you can interact via text to the mark 1:
`python -m mycroft.client.text.main --quiet`
