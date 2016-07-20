---
title: Core Overview
taxonomy:
  category:
    - docs
---

As talked about in the [getting started section](), Mycroft Core contains four main services - 
the messagebus, the skills service, the speech client, and the command line interface. Only one 
of the command line client and speech client need to be run, as they both provide methods of interacting with Mycroft.
This section will cover what these services actually do, first in a fairly high level overview, and then on a more technical level.

## Overview

 - A user says a phrase including the wakeword (`Hey Mycroft` by default)
 - The speech client strips out the wakeword and sends the audio to a speech to text service (Google STT by default)
 - The speech to text service sends back the parsed text, which is sent on the messagebus by the speech client
 - [Adapt](https://adapt.mycroft.ai/) gets the text and tries to match it to an intent registered by one of the skills
 - If it succeeds, the intent it finds is sent on the messagebus, along with what keywords it found
 - The skills service picks up the message and gives it to the skill matching the intent
 - The skill processes the message, does some action with it, and sends any message to be spoken on the messagebus
 - The speech client takes the message and sends it to a text to speech service ([Mimic](https://mimic.mycroft.ai/) by default) 

## Messagebus

The messagebus is how all of the different parts of Mycroft communicate between each other. It does this by sending different
types of messages that contain needed information. For example, one part of Mycroft could send a `speak` message that contains
something for Mycroft to say. The message would be carried over the messagebus, and any other service connected to it could read
the message and parse it. In our case, the speech or command line client would pick up the messsage and then convert it into speech.

The messagebus is also hosted as a websocket that other things can communicate with. By default, this websocket is set on 
`localhost:8000/events/ws`.

## Speech Client

tbd

## Skills



