---
title: Core Overview
taxonomy:
  category:
    - docs
---

As talked about in the [getting started section](), Mycroft Core contains four main services - the messagebus, the skills service, the speech client, and the command line interface. Only one of the command line client and speech client need to be run, as they both provide methods of interacting with Mycroft. This section will cover what these services actually do on a general level.

## Overview

 - A user says a phrase including the wakeword (`Hey Mycroft` by default)
 - The speech client strips out the wakeword and sends the audio to a speech to text service (Google STT by default)
 - The speech to text service sends back the parsed text, which is sent on the messagebus by the speech client
 - [Adapt](https://adapt.mycroft.ai/) gets the text and tries to match it to an intent registered by one of the skills
 - If it succeeds, the intent it finds is sent on the messagebus, along with what keywords it found
 - The skills service picks up the message and gives it to the skill matching the intent
 - The skill processes the message, does some action with it, and sends any message to be spoken on the messagebus
 - The speech client takes the message and sends it to a text to speech service ([Mimic](https://mimic.mycroft.ai/) by default) 
 
The command line client essentially shortcuts directly to sending the text to Adapt, as there is no speech to text service required. It also handles sending a `speak` message to the chosen text to speech service, like the speech client does.

## Messagebus

The messagebus is how all of the different parts of Mycroft communicate between each other. It does this by sending different types of messages that contain needed information. For example, one part of Mycroft could send a `speak` message that contains something for Mycroft to say. The message would be carried over the messagebus, and any other service connected to it could read the message and parse it. In the core, the speech or command line client would pick up the messsage and then convert it into speech. 

The messagebus is also hosted as a websocket that other things can communicate with. By default, this websocket is set on 
`localhost:8000/events/ws`.

## Speech Client

There are a few components to the speech client. There is the `AudioConsumer`, `AudioProducer`, and within that the `listener`. There exists a shared queue of audio files between the consumer and producer. The producer grabs segments of audio from the listener and the consumer uses the audio to send to an external STT engine and emit the result as an `utterance`.

### Listener

The listener figures out what pieces of audio Mycroft should record and respond to. It first detects its wake word using pocketsphinx on around the last two seconds of audio. Audio older than two seconds is discarded. After detecting its wakeword it begins recording until when it thinks the user has finished speaking. This is estimated using a heuristic described below.

#### Phrase Heuristic

Essentially, the listener records until the "noise level" falls at or beneath `0`. The "noise level" is a sort of estimate of the relative noise in the past few seconds. Every time the noise is above a certain threshold, the "noise level" increases. On the contrary, the opposite happens when the noise is lower than the threshold. By keeping track of this number, small separated noises will not affect the noise level as much as long contiguous noises most likely indicative of voice.

Another technique the listener uses is waiting for audio when it knows there should be more. If you say the wake word without any following noise Mycroft will wait for input for another 3 to 4 seconds. The sum of audio that is above the threshold is maintained while recording a phrase. The audio will only return when both the noise level is at 0 and the length of audio above the threshold is past a minimum amount (however, after 30 seconds the listener will time out and return anyways).

## Skills Service

The skills service has two main components - the skills themselves and the Adapt intent parser.

### Skills

A skill consists of `vocabulary` files (a list of phrases or words that Mycroft should respond to), `dialog` files (a list of phrases that Mycroft will say in response to something in the skill), and a Python file. This Python file determines how the vocabulary maps to each intent, as well as what actions Mycroft will take when an intent is found (ranging from saying something to turning off the lights). 

### Adapt

In short, Adapt takes in a sentence and attempts to find what the intent of it is by looking for matching words and phrases from intents and vocab registered by different skills. Adapt is described in more detail in [its documentation](https://adapt.mycroft.ai/)

 
