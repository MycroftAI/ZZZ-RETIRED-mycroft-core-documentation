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



