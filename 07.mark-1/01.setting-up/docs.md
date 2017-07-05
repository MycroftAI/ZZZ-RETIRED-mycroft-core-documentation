---
title: Getting Started
taxonomy:
    category:
        - docs
---

# Setup Instructions

There is a overall setup pdf located [here](https://mycroft.ai/to/user-guide/) with instructions on setting up the Mark 1.

# Changing Password
It is a good idea to change the password.  By default the user is `pi` and the password is `mycroft` for the mark 1.  In order to change this you would ssh to it or connect a hdmi cable to the port on the back of the Mark 1 unit.

From the console/ssh session enter the following command:
`passwd`

It will prompt you for the current password, then new password twice, and then the new password will be saved.

example output:
```
Changing password for pi.
(current) UNIX password:
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

# Setup ssh keys

# Checking for installed skills
From the ssh/console session run the following command to see a list of installed skills, hit spacebar to scroll through:

`msm list | sort | more`

# Log File Locations
All mark 1 logs are located in `/var/log/mycroft-` then different names for different logfiles.

All of these log file locations you can view by running:
`cat logfile | more` Use Spacebar to step through the results, q will quit the file.

You can also live view the log by tailing it with:
`tail -f logfile` This will live tail the log and anytime something is written you will see it
`cntrl + c` will stop it.


## Skill Log
The skill log which includes information about skills loading, api calls for updates/configuration changes can be found at:

`/var/log/mycroft-skills`

## Speech Log
This contains log information about words being spoke, wake words heard, etc.

`/var/log/mycroft-speech-client.log`
