---
title: Core Overview
taxonomy:
  category:
    - docs
---

Mycroft Core contains four main services - the messagebus, the skills service, the speech client, and the command line interface. Only one of the command line client and speech client need to be run, as they both provide methods of interacting with Mycroft. This section will cover what these services actually do on a general level.

## Overview

 - The user says the wakeword (`Hey Mycroft` by default)
 - The speech client records the subsequent spoken audio and send it to the Mycroft backend (by default) to perform speech to text
 - The speech to text service sends back the transcription, which is sent on the messagebus by the speech client
 - The skill client catches the message and uses [Adapt](https://adapt.mycroft.ai/) to match it with an intent registered by one of the skills
 - If it succeeds, the intent is sent on the messagebus along with what keywords it found
 - The skills service picks up the message and gives it to the skill matching the intent
 - The skill processes the message, performs any appropriate action, and sends any message to be spoken on the messagebus
 - The speech client takes the message and sends it to a text to speech service ([Mimic](https://mimic.mycroft.ai/) by default) 
 
The command line client essentially replaces the first two steps, directly sending text onto the messagebus as there is no speech to text service required. It can also handle sending a `speak` message to the chosen text to speech service, like the speech client does.

## Messagebus

The messagebus is how all of the different parts of Mycroft communicate between each other. It does this by sending different types of messages that contain needed information. For example, one part of Mycroft could send a `speak` message that contains something for Mycroft to say. The message would be carried over the messagebus, and any other service connected to it could read the message and parse it. In the core, the speech or command line client would pick up the messsage and then convert it into speech. 

The messagebus is also hosted as a websocket, so other applications can monitor and communicate with Mycroft. By default, this websocket is set on 
`localhost:8181/core`.

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

In short, Adapt takes in a sentence and attempts to find what the intent of it is by looking for matching words and phrases from intents and vocab registered by different skills. Adapt is described in more detail in [its documentation](https://adapt.mycroft.ai/).

 
