---
title: Mycroft Skills Framework
taxonomy:
    category:
        - docs
---
The Mycroft Skills Framework is intended to allow you to develop skills by attaching your local developer code to a running Mycroft device (or MessageBus Service). By default, it will assume that you have a messagebus service running locally on port 8000, and you would drive your skill with a cli or speech client attached to the same message bus.

This doc assumes you're working in an isolated virtualenv for your skill. You can also choose to install the sdk into your global python install with sudo.

## Installing the skills SDK
```
pip install mycroft_skills_sdk --extra-index-url=http://pypi.mycroft.team --trusted-host pypi.mycroft.team
```

## Managing your dependencies
The skills container will expect the dependencies for your skill implementation to be installed via pip into a directory named "lib", which lives inside your current working directory. Install your requirements.txt file via pip
```
pip install -t lib -r requirements.txt
```

## Running your skill
```
mycroft-skills-container ./path/to/skill/root
```

## Running a Mycroft skill in isolation
```
mycroft-skills-container ./mycroft/skills/weather
```

## Running a skill without the mycroft skills service
Mycroft Intent Determination runs as a skill. In order to test a skill in the container without the skills service, the container can also run an instance of the intent skill.

```
mycroft-skill-container ./mycroft/skills/weather --enable-intent-skill
```
