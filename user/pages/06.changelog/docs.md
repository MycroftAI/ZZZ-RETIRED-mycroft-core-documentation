---
title: 'Changelog'
taxonomy:
    category:
        - docs
---
[github-releases]:https://github.com/MycroftAI/mycroft-core/releases
[View the releases on GitHub here.][github-releases]

# v0.7.8

### Base media skill
Thanks to [forslund](https://github.com/forslund) for his new base media class for developers to extend from. We think this will provide a more cohesive experience for all media skills, as they will all have similar behavior.

### Weather display on enclosure
This release also brings in a new piece of integration with the unit. When asked what the weather is, Mycroft will now display what the conditions currently are as well as what the current temperature is. This marks further improvement in enhancing the experience on the device.

### Bug fixes

- We fixed a bug where it would send `what 's` rather than `what's` to Wolfram Alpha, resulting in unintended behavior.
- We added the new media skill to the list of blacklisted skills in the skill loader so that it wasn't trying to load an effectively empty skill.
- We updated the `load_data_files` function to also load regex files, so that developers only need to call one function to load all of the files they need.

# v0.7.7
This update includes a few updates to the integration between the device's faceplate and skills, as well as some minor configuration changes.

### Device changes
We've continued our integration of the faceplate with skills by updating it to work with the stock skill. Now, when you ask Mycroft what the stock price of a company is, he will display the company ticker and price, just like a traditional stock display.

We've also started improving the user experience on the device by removing some of the delay with interacting with the button. Previously, when you pressed the button to stop a skill, you often had to wait a few seconds before it would actually stop. Now, skills should stop much more quickly.

### Wakeword configuration
We've received many questions about changing your Mycroft's name so that it will respond to whatever you want. Listening to your feedback, we've made this configuration process much easier than before. Now, all you need to do is put the new name in the configuration file, as well as its pronunciation. Take a look at our [documentation](https://docs.mycroft.ai/development/troubleshooting.notes#how-do-i-change-what-mycroft-responds-to) for more.
