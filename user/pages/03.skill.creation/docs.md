---
title: Creating a skill
taxonomy:
    category:
        - docs
---

# Creating a skill

## Setting up the folders

Once you've come up with your idea for a skill, make a new folder in `mycroft-core/mycroft/skills` with the desired skill name. Please note that this folder name should be lower-case, and do not use the names of frequently used python modules such as `time` to avoid conflicts.

For skills, there should generally be four things inside this folder - a folder called `dialog`, a file called `__init__.py`, a folder called `test`, and a folder called `vocab`. You can also optionally have a `regex` folder, used to define regex phrases for more flexible vocab. The folder structure should look like this:
```
- my-skill-name
-- dialog
-- regex
-- test
-- vocab
-- __init__.py
```

### Dialog
The `dialog` folder contains subfolders for each spoken language the skill supports, each of which has `.dialog` files for what Mycroft should say when he executes a skill. The general structure looks like
```
-dialog
--en-us
---my.file1.dialog.
---my.file2.dialog
--pt-br
---my.file.1.dialog
---my.file.2.dialog
```

Take a look at the [Hello World Skill](https://github.com/MycroftAI/mycroft-core/tree/master/mycroft/skills/helloworld) as an example. Its `dialog` folder has an `en-us` subfolder in it, which corresponds to American English. Inside are three dialog files. As an example, look inside `welcome.dialog`. It looks like
```
Any time.
Glad to be of service.
Glad to help.
My Pleasure.
No problem.
You're welcome.
```
Note that Mycroft will not say all of these things when the skill is executed. Instead, he randomly chooses from each of the lines in the file to determine what to say.

There are generally seperate .dialog files for each intent defined in the skill.

### `__init__.py`
`__init__.py` is where you put the actual bulk of the skill, including a class that inherits from the MycroftSkill class and contains functions that pertain to how the skill operates. For now, just create an empty `__init__.py` file.

### Vocab
The `vocab` folder contains subfolders for each language supported, like `en-us`. Inside each language folder, we place `.voc` files which contain phrases or keywords that determine what Mycroft will listen for to trigger the skill.
```
-vocab
--en-us
---my.file.voc.
--pt-br
---my.file.voc
```

Looking at the [Hello World Skill](https://github.com/MycroftAI/mycroft-core/tree/master/mycroft/skills/helloworld) again, there is a `ThankYouKeyword.voc` file in the `en-us` folder that contains the vocabulary for the thank you intent in the Hello World Skill. It contains a list of keywords and phrases that trigger the intent, and looks like the following:
```
thank you
thanks
```
In this case, whenever a user says either `thank you` or `thanks`, Mycroft will be able to identify that those phrases are related to the Hello World Skill, and trigger the logic for that skill.

There are generally seperate .voc files for each intent, and sometimes multiple files per intent.

### `Regex`
The `regex` folder contains subfolders for each supported language, such as `en-us`. Inside of each of these subfolders are `.rx` files that contain regular expressions to create more flexible keywords for intents.
```
-regex
--en-us
---my.regex.rx
--pt-br
---my.regex.rx
```
As an example of how to use this, take a look at the [weather skill](https://github.com/MycroftAI/mycroft-core/tree/master/mycroft/skills/weather).  In the `regex/en-us` folder, there is a `location.rx` file that defines a regular expression for the group `Location`. It looks like this:
```
(at|in) (?P<Location>.*)
```
This can be hard to parse, especially for people who have never seen regular expressions before. Regular expressions are essentially formatted pieces of text that can be used to match a wide range of phrases or strings. The chunks of text inside parentheses are called capturing groups, and are used to group similar things. For example, `(at|in)` is a group that will match either the word `at` or the word `in`. The block `(?P<Location>.*)` is more complicated. Like `(at|in)`, it is also a capturing group. However, the `?P<Location>` syntax is used to give a name to whatever it captures, which is very useful for our purposes. In this case, it gives it the name `Location`. The following two characters, `.*`, are what are used to define what this group captures. The dot character, `.` can be used in regex to represent any character except for newlines. The `*` special character is used to repeat something zero or more times. So together, `.*` matches zero or more characters of any kind. This means that the regex `(at|in) (?P<Location>.*)` will match something like `in London`, as well as `at the corner store`. In the first case, the `Location` is London, and in the second, the `Location` is `the corner store`. 

Regular expressions are very powerful and also quite complicated, and this has only explained a small part of them. Look through a [regex tutorial](http://www.regular-expressions.info/repeat.html) if you want to learn more.

### `Test`
The `test` folder contains a subfolder for intent, inside of which are `.intent.json` files. These are used to test whether your code properly creates intents.
```
-test
--intent
---sample1.intent.json
```

## Creating your first skill

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

## Testing your skill
Creating tests is an essential part of making your skill, and ensures that you have properly created your skill and that Mycroft can determine your intents from a sample phrase.

### Creating tests
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
