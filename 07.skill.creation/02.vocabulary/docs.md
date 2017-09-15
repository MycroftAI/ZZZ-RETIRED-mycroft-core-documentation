---
title: Fun with .voc files
taxonomy:
    category:
        - docs
---


The Adapt Intent parser has the ability to handle multiple vocabulary files. It also can parse sentences to find the key words. This means that vocabulary files need only focus on keywords, not specific uterances. 


For a good example of this, look at the Alarm Skill on Github:
[Alarm](https://github.com/MycroftAI/skill-alarm)




Notice the different .voc files. For the AlarmSKillKeyword.voc file:

````

timer
timers
alarm
alarms
````

In this example:
"Set an alarm for 5 minutes from now",
"Alarm 5 minutes", and "5 minute timer"
all set an alarm for 5 minutes from now.


Keep this in mind when designing skills.
