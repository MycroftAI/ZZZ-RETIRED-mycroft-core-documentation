---
title: Your First Skill
taxonomy:
    category:
        - docs
---

## Creating your first skill

For this we will still be going over the Hello World Skill from Github:
[Hello World Skill](https://github.com/MycroftAI/skill-hello-world)

### Header
When creating the skill, you need to start by importing the proper libraries for use in skills. 

```python
from os.path import dirname

from adapt.intent import IntentBuilder
from mycroft.skills.core import MycroftSkill
from mycroft.util.log import getLogger
```

`dirname` is used so that the class knows what files are in the current directory. Specifically, this is so that it can access the `.dialog` and `.voc`files.
IntentBuilder is used to register your new "intent", which is how Mycroft interprets what you say to determine what to do. A single skill can have many intents. For example, the Hello World skill has three intents.
MycroftSkill is the class that your skill will inherit from.
getLogger is a wrapper for the python `logging` object that is used to log errors or relevant information.

You can then put your name as the `__author__` variable and create a logger for use in debugging.
In the Hello World skill, this looks like

```python
__author__ = 'eward'

LOGGER = getLogger(__name__)
```

### Creating the class

You then declare the class as inheriting from MycroftSkill and declare its various member functions.

In the hello world skill, the general outline looks like
```python
class HelloWorldSkill(MycroftSkill):
    def __init__(self):
    
    def initialize(self):
    
    def handle_thank_you_intent(self, message):
    ...
    def stop(self):
    
def create_skill():
    return HelloWorldSkill()
```
Each of these functions does something different.

#### __init__
This is the constructor for the class, called when a new <skillname> object is created. In it you should call the constructor of the MycroftSkill class using `super` and initialize any member variable to the values you need.r
In the Hello World skill, this looks like
```python
def __init__(self):
        super(HelloWorldSkill, self).__init__(name="HelloWorldSkill")
```

#### initialize
This is where you should load all of the files in the directory and build each intent you want to create. Note that if you want to use regex in your skill, you must also call the inherited method `self.load_regex_files(path)`
For the Hello World skill, this looks like
```python
def initialize(self):
    self.load_data_files(dirname(__file__))

    thank_you_intent = IntentBuilder("ThankYouIntent").\
        require("ThankYouKeyword").build()
    self.register_intent(thank_you_intent, self.handle_thank_you_intent)
    ...
```
This creates an intent named thank_you_intent that requires a ThankYouKeyword, which is one of the phrases in the ThankYouKeyword.voc files. You can also require defined regex entities, such as `Location` in the regex example.
It then registers that the function handle_thank_you_intent is what should be called if the ThankYouKeyword is found.
All of the other intents are registered in the same way.

#### handle_<intent_name>_intent
This is where you tell Mycroft to actually do what you want him to do. This can range from something like a call to an API to opening an application. In the Hello World skill, each intent simply tells Mycroft to speak from the dialog file..
```python
def handle_thank_you_intent(self, message):
    self.speak_dialog("welcome")
```
This simply tells Mycroft to randomly select one of the pieces of dialogue from the welcome.dialog file and speak it. 
In your skill, you can include as many ways of phrasing what he says as you want.

Note that in most Mycroft skills, the `handle_intent` function will include an API call or something else with a potential failure case, so it is best to enclose what you want to run in a `try`/`except` block.
Note also that it always takes two arguments, self and message, even if you never use message.

#### stop
This function is used to determine what Mycroft does if `stop` is said while this skill is running. In the Hello World skill, since Mycroft is saying simple phrases, the stop function just contains the word pass:
```python
def stop(self)
    pass
```
The keyword `pass` does nothing when executed. It is simply used when code is required syntactically but you do not want any code to run.
For an example of a skill that uses the stop function, look at the [NPR News skill](https://github.com/MycroftAI/mycroft-core/tree/master/mycroft/skills/npr_news).

#### create_skill
This is outside of the class definition, and is used to actually create a skill object when the script is called.

## The Test folder and Intents
Intents translate sentance structure into machine code, in this case, JSON files. These live within the Test folder of your skill structure.

NOTE: We are still working on testing capabilities in order to create more robust skills.

### Creating intents
Intent tests take the form of an `.intent.json` file with a structure inside that determines whether a particular intent is found. Take a look at the first test file, `sample1.intent.json` in the Hello World skill.
```
{
  "utterance": "Thank you",
  "intent_type": "ThankYouIntent",
  "intent": {
    "ThankYouKeyword": "thank you"
  }
}
```
`utterance`: This is the sample phrase that you would say to Mycroft, and that should trigger your intents.
`intent_type`: This is the type of intent that should be found in your sample utterance.
`intent`: In this structure, you should list each keyword defined by your skill that should be found in the utterance.
