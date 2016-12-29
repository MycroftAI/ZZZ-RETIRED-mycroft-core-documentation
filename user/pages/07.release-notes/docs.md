---
title: 'Release Notes'
taxonomy:
    category:
        - docs
---
[github-releases]:https://github.com/MycroftAI/mycroft-core/releases
[View the releases on GitHub here.][github-releases]

# v0.8.0
### New API and web service integration
- Connenction to the new account management back-end. We have moved to [home.mycroft.ai](https://home.mycroft.ai) from [cerberus.mycroft.ai](https://cerberus.mycroft.ai). Older code is incompatible with the new API so we will continue to maintain Cerberus for some time. Not sure where to pair? Let Mycroft tell you the correct website.
- Many more configuration options, including support for multiple social media login types as well as stand-alone accounts.
- Change TTS engine, wake-word, units, time and date format, and more settings from the web interface.
- We lost support for loading location and timezone configuration from the web but this is coming again soon. These settings can still be found in the mycroft.conf file; [Take a look here.](https://github.com/MycroftAI/mycroft-core/blob/master/mycroft/configuration/mycroft.conf#L3)

### Core enhancements
- Major configuration format refactor. The flat mycroft.ini file has now been replaced by a json implementation in mycroft.conf. This should allow for simpler usage and will be much more powerful.
- The identity.json has been renamed to identity2.json, to avoid conflicts with the Cerberus account management system.
- Configuration loading changes: home.mycroft.ai will periodically be polled poll for changes and no longer requires a complete restart for settings changes to take effect.
- Wolfram Alpha and Open Weather Map now have a isolated API layer, we need not package those libs.
- The listening process has been refined, removing unnecessary threads for better performance.
- The message bus websocket port and path have changed to avoid conflicts. Mycroft now listens on port 8181 with the route '/core'

### Mycroft Mark 1 unit enhancements
- Our unit specific enclosure client (for updating Arduino sketches) and packaging method have been modified for platform detection either by configuration file or from serial port communication. This will allow for better compatibility for other systems, such as standalone Raspberry Pi's.

# v0.7.20
### Wifi Setup Client (for Mycroft unit)
- When no internet connection found (usually during STT) the instructions now direct user to press button on the unit
- Added auto-check for internet connection on bootup
- Wifi local access point activates at start, user gets guided into connecting
- Once connected to access point, captive web portal allows selection and configuration of desired wifi

# v0.7.18 / v0.7.19
- First pass of wifi setup, recalled

# v0.7.17

### Push to Talk
- Pressing the button when it isn't listening starts it listening
- Pressing the button when listening will stop the listen
- Added a mycroft.util.signal() mechanism for out-of-thread communication
- Pressing the button now creates an "buttonPress" signal from the Enclosure.  The viseme playback and aplay check for the 'buttonPress' signal to abort.

### Misc
- Removed "Sorry I didn't catch that", irritating during false activations
- added configuration for the Mimic TTS engine to change speech speed
- ArchLinux build script changes
- Introduced (but didn't enable) the wifisetup client

# v0.7.16

- Added support to the Enclosure API for the visualization of Text to Speech (using "visemes")
- Mycroft's default Mimic text to speech support now sends visemes to the Enclosure.  On a Mycroft unit, this produces lip syncing on screen when it speaks

This integrates changes from the last enclosure code release:

- Illumination changes also impact the matrix dispaly
- Added visemes, which will be visible once changes are made to the TTS client
- Removed the weather icons, added a generic mechanism for sending encoded icons across the serial line

It also breaks display of text and sprites, see https://github.com/MycroftAI/mycroft-core/issues/358
This will be addressed in an upcoming release.


# v0.7.15

Refined the enclosure menu behavior:
- Menu now comes up after pressing the button for 3 seconds
- Reordered the menu
- Added Illum menu item, which controls the brightness of the eyes
- Several minor visual refinements to the menu

# v0.7.14

### Hardware Changes
- Hardware units now show a spinning eye animation when shut down, rebooted, or turned on, and stop displaying it when power is fully on or off
- When volume is changed using the unit encoder dial, the eyes now display the current volume (0-11) for a few seconds, then reset to normal
- By holding down the encoder button on a unit for five seconds, users can access menu mode, which allows power control (reboot and shutdown), factory reset, and the hardware test (replacing the automatic hardware test trigger), and will soon include wi-fi setup

### Other Changes
- Volume levels can now be configured by the user to determine what each level (0-11) corresponds to
- Mycroft's speech is now broken up into smaller individual chunks, making it easier to understand


# v0.7.13

### Wolfram Changes
With this new release, the Wolfram Alpha Skill now gives much more concise responses. Rather than reading several definitions for a word, Mycroft will only read the first. Along with that, when Wolfram cannot find anything for a particular query, rather than speaking the result from the Did you mean? query, he simply mentions he could not find any results but did find something for an alternative query.

### Hardware Test
This release also brings in a basic hardware test. When activated by holding the button for 5 seconds, Mycroft will now run through tests to verify that the display, knob, microphone, and speaker are all working properly.

# v0.7.12

This is a patch release to fix an issue with the manifest file, preventing the new volume sound from being included in the packaging.

# v0.7.11

This is a patch release to fix an issue that was preventing avrdude from uploading Arduino code to the Mycroft unit.

# v0.7.10

This release includes some less visible changes and fixes. These changes and others coming soon will allow us to better iterate the development of mycroft-core, integrate multiple build systems, and decouple skills from the process.

### Volume changes
If you have a Mycroft unit, the volume behavior has changed. Delay has been decreased and instead of speaking the volume level setting at each click, a simple sound has been added. This reduces the chance of turning the dial several notches and then waiting for Mycroft to stop speaking. He will still speak if you set the volume with voice control.

### Enclosure improvements
The enclosure code is in the process of some heavy refactoring, but some quick fixes were added to make it more responsive and tweak the weather animation.

### Tweaks
We have also separated packaging scripts from this repository, so they are no longer tied to a release. This also reduces some clutter and opens the possibility to download daily master builds via apt. Check back for an update at http://docs.mycroft.ai.

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


