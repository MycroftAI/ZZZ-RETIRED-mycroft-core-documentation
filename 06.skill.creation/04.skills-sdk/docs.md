---
title: Skills SDK
taxonomy:
    category:
        - docs
---

## What Makes a Skill
A skill is a class that extends the [MycroftSkill](https://github.com/MycroftAI/mycroft-core/blob/master/mycroft/skills/core.py#L98) class. It is instantiated by the skills container via a [create_skill](https://github.com/MycroftAI/mycroft-core/blob/master/mycroft/skills/spelling/__init__.py#L33) method on the skill module. See Mycroft's [spelling skill](https://github.com/MycroftAI/mycroft-core/blob/master/mycroft/skills/spelling/__init__.py) for a simple example.

## Running your skill
* Find the IP of your mycroft unit (try asking mycroft what its IP address is)
* Create a virtualenv and a clean directory for your skill.
  * install the skills SDK via the instructions [here](https://github.com/MycroftAI/mycroft-core/wiki/Mycroft-Skills-Framework#installing-the-skills-sdk)
* Implement a skill. Try copying the spelling skill's __init__.py into your directory.
* Install your dependencies as instructed [here](https://github.com/MycroftAI/mycroft-core/wiki/Mycroft-Skills-Framework#managing-your-dependencies)
* Log into your mycroft, and stop the skills service (so there's only one of the spelling skill running)
```
sudo /etc/init.d/mycroft-skills stop
```
* Launch the skills container, instructing it to connect to your mycroft unit. Since the skills service has been stopped, we'll also need the container to run the intent skill as well.
```
mycroft-skills-container --messagebus-host=<MYCROFT IP ADDRESS> --enable-intent-skill
```
* Try your skill through your mycroft unit.
```
Hey mycroft, spell calamity
```
