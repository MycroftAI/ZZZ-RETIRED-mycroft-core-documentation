---
title: 'Startup Cheatsheet'
taxonomy:
    category:
        - docs
---


#Mycroft Terminal Commands Cheatsheet
These are some helpful commands to interact with Mycroft through a terminal. You can always call each with the phrase "help" to get more info.

##Start Mycroft
###All at once
`./mycroft.sh start`
###One piece at a time
In separate terminals:  
`./start.sh skills`  
`./start.sh service`  
`./start.sh voice`  

##Interact with Mycroft through the CLI

###Once Started
`./start.sh cli --quiet`

###From not-started
`./mycroft.sh start -d`

##Stopping Mycroft
`./mycroft.sh stop`