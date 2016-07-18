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
We continued our integration of the faceplate with skills by updating it to work with the stock skill. Now, when you ask Mycroft what the stock price of a company is, he will display the company ticker and price, just like a traditional stock display.

We also started improving the user experience on the device by removing some of the delay with interacting with the button. Previously, when you pressed the button to stop a skill, you often had to wait a few seconds before it would actually stop. Now, skills should stop much more quickly.

### Wakeword configuration
We've received many questions about changing your Mycroft's name so that it will respond to whatever you want. Listening to your feedback, we've made this configuration process much easier than before. Now, all you need to do is put the new name in the configuration file, as well as its pronunciation. Take a look at our [documentation](https://docs.mycroft.ai/development/troubleshooting.notes#how-do-i-change-what-mycroft-responds-to) for more.

# v0.7.6

### Listener improvements
We've improved the listener in various ways this week. Specifically, there is now a significant drop in false positives in detecting the wakeword, making it so that Mycroft will respond less to phrases that don't contain `Hey Mycroft`.

To go along with these changes, we've also changed the wakeword from `Mycroft` to `Hey Mycroft` in order to make Mycroft more responsive.

### Sleep skill improvements
We also improved the sleep functionality of Mycroft. He will now respond much more consistently to `wake up`, rather than also waking up on other phrases like he did before.

### Wolfram Alpha skill improvements
Previously, queries to Wolfram would fail when it thought that there were other possible alternatives to the query said. Now, the Wolfram Alpha skill will now search again for the first suggested alternative, which increases its responsiveness.

Additionally, the WA skill will now properly reply to you when you say something like `what's a tangram`. Before, it would repeat the entire query back to you. Now, it parses your query to give a more natural response.

Finally, we removed the `I am searching for...` message, as it was frequently increasing response time, and sounded unnatural. We replaced it with the more natural `Sorry, I didn't find a response for...` on failure. 

### New animations
We've added a "thinking" animation to displayed on the faceplates of units while they wait to get information.

# v0.7.4

### New skills
We added three new skills this week - a stock skill that will give you stock prices of companies, a speak skill that will repeat what you say back to you, and a personal skill that allows Mycroft to tell you more about himself.

## Wolfram responsiveness
We significantly increased the amount of times that the Wolfram skill will give back a useful result.

### Unit integration
This update comes with more integrations with the unit and skills. Mycroft will now spell a word on his faceplate when you ask him to spell a word. 


