---
title: Adding New Skills
taxonomy:
  category:
    - docs
---

##How to add new skills

Mycroft AI is a community project. What does this mean? It means we rely on community members to come up with good use-cases as skills. While Mycroft comes with some functionality out of the box, you can always add more community-written skills. 

With that comes a minor caveat of a lot of these skills not being fully tested. Some also don't work, but we keep them in the repo as examples to everyone. 

Adding a new skill is as easy as using git clone on a repo to your skills folder. This varies from device to device. For example, there is a shortcut to the **skills** folder in the Home directory of the Raspberry Pi. This shortcut points to 
```
/opt/mycroft/skills
```

This is also the same location as [Git-Clone install](), but double check the git wiki for your enclosure to be sure.


To add a new skill, head over to the [mycroft-skills repo](https://github.com/MycroftAI/mycroft-skills). From there, clicking on submodules of skills takes you to the original authors repo.

Once you find the skill you want, cd into your skills directory:
````buildoutcfg
cd /opt/mycroft/skills
````
and use the git clone command. For the Daily meditation skill, for example, you would use this command:
````buildoutcfg
git clone https://github.com/kfezer/daily_meditation.git
````
This will create a new daily_meditation folder in your skills folder. Mycroft should automatically add any newly added skills.


## Easier install! Use MSM!
If you're running a Picroft unit, you can also try msm, or the Mycroft Skills Manager. For the example above
````buildoutcfg
msm install https://github.com/kfezer/daily_meditation.git
````
does the same work.
