---
title: Creating a skill
taxonomy:
    category:
        - docs
---

It is easy to develop skills for Mycroft. The most important part is to understand the structure of each skill. 


## Setting up the folders

Once you've come up with your idea for a skill, make a new folder in `opt/mycroft/skills` with the desired skill name. Please note that this folder name should be lower-case, and do not use the names of frequently used python modules such as `time` to avoid conflicts.

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

Take a look at the [Hello World Skill](https://github.com/MycroftAI/skill-hello-world) as an example. Its `dialog` folder has an `en-us` subfolder in it, which corresponds to American English. Inside are three dialog files. As an example, look inside `welcome.dialog`. It looks like
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


Regular expressions are very powerful and also quite complicated, and this has only explained a small part of them. Look through a [regex tutorial](http://www.regular-expressions.info/repeat.html) if you want to learn more.

### `Test`
The `test` folder contains a subfolder for intent, inside of which are `.intent.json` files. These are used to test whether your code properly creates intents.
```
-test
--intent
---sample1.intent.json
```
