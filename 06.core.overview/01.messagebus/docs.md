---
title: Messagebus Overview
taxonomy:
  category:
    - docs
---

This is a more in-depth look at the messagebus, intended for use by developers or anyone else who wants to understand how it works.

## Implementation
The messagebus relies on a Python library called [pyee](https://github.com/jfhbrook/pyee). This adds a new `EventEmitter` class that you can import. The functionality of this class is fairly simple, and consists of two main functions. From the pyee documentation:
```
ee.on(event, f=None): Registers the function f to the event name event. Example:

ee.on('data', some_fxn)

If f is not specified, ee.on returns a function that takes f as a callback, which allows for decorator styles:

@ee.on('data')
def data_handler(data):
    print data
    
ee.emit(event, *args, **kwargs): Emits the event, calling the attached functions with *args. For example:

ee.emit('data', '00101001')

This will call data('00101001')' (assuming data is an attached function). Returns False if no functions are attached to handle the emission (otherwise True).
```

This behavior is essential to how Mycroft works. By registering different types of messages to emitters, we can then call functions from multiple places just by emitting messages of certain types. 

We don't just directly emit messages, however. We have our own `Message` class that has attributes `message_type` and `metadata`. Note that `metadata` is a Python dict. You can read more about how to interact with these [here](https://docs.python.org/2/library/stdtypes.html#mapping-types-dict). You can create a Message object with something like `Message('speak', metadata={'utterance': 'Hello world'})`. When this is emitted by one of the emitters in Mycroft-Core, it is automatically converted into JSON to be sent across the messagebus. Once the message is received, it is then converted back into a Message, and is emitted again with the `message_type` as the event. __This means that when emitting something directly, you should emit a Message object with the message_type as the event you want, and the metadata as the information you want to include. To handle an event, use the message_type as the event name.__

You can emit whatever you want across the messagebus. Note, however, that there are currently a few message types that are currently emitted and tied to parts of Mycroft core functionality, as listed below.

## Message types

| Message Type        | Sent from           | Purpose | Contents |  Example Metadata |
| ------------- | ------------- | -----            | ------------ | ---------- |
| detach_intent      | The `detach` function of MycroftSkill  | Detaches the intent specified  | The name of the intent to be detached |`{'intent_name': 'HelloWorldIntent'}` |
| any intent      | The intent skill after determining the intent of an utterance. | Calls the handler for that intent. Note that the metadata needed depends on the skill.  | The name of the intent and the needed metadata |`{"HelloWorldKeyword": "hello world", "intent_type": "HelloWorldIntent", "utterance": "hello world", "confidence": 1.0, "target": null}` |
| intent_failure | The intent skill after failing to determine the intent of an utterance | Sends the utterance to the Wolfram Alpha skill | The utterance | `{"utterance": 'hello world'}` | 
| message      |  The messagebus client after receiving a message | Logs the json dumps of the message in the terminal  | A Message object | A Message object  |
| mycroft.media.stop      | Any skill that inherits from the media base class | Stop anything playing on a media skill | The skill where the message originated  | `{'origin': 'MediaSkill'}` |
| mycroft.paired      | The pairing skill  | Used to give updates on pairing process | Whether the device is paired or not |`{'paired': True}` |
| mycroft.stop      | The stop skill | Calls the `stop` function of any skill currently running. | N/A  | N/A |
| recognizer_loop:audio_output_start      | The speech service | Show when Mycroft starts talking | N/A  | N/A |
| recognizer_loop:audio_output_end      | The speech service | Show when Mycroft stops talking | N/A  | N/A |
| recognizer_loop:record_begin      | The listener after the wake word is detected | Show when Mycroft starts recording | N/A |N/A |
| recognizer_loop:record_end      | The listener after finishing recording | Show when Mycroft stops recording | N/A  | N/A |
| recognizer_loop:sleep      | The sleep skill  | Causes the listener to not send audio until `Hey Mycroft, wake up` is heard | N/A | N/A |
| recognizer_loop:utterance      | The listener, once the STT has transcribed the audio | The intent skill parses it to determine intent | The words transcribed by the STT service | `{'utterances': 'Hello world','session': 'some_unique_id'}` |
| recognizer_loop:wakeword      | The listener  | Show when the wakeword was detected | What the wakeword is  | `{'utterance': 'Hey Mycroft', 'session': 'some_unique_id'}` |
| register_intent      | Each skill that registers an intent | Registers the intent with the intent skill  | The intent and any other needed information for the skill | `{"at_least_one": [], "requires": [["HelloWorldKeyword", "HelloWorldKeyword"]], "optional": [], "name": "HelloWorldIntent"}` | 
| register_vocab      | Each skill that registers vocab | Registers the vocab with the intent skill | The vocab phrase and what type of keyword it is | `{"start": "hello world", "end": "HelloWorldKeyword"}` | 
| speak      | Any part of the core that needs to say something | Speaks the utterance | The phrase to speak | `{"utterance": "Hello"}` | 
