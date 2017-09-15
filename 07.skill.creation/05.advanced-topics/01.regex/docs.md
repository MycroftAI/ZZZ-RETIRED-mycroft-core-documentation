---
title: Regex
taxonomy:
    category:
        - docs
---

### `Regex`
The `regex` folder contains subfolders for each supported language, such as `en-us`. Inside each of these subfolders are `.rx` files that contain regular expressions to create more flexible keywords for intents.
```
-regex
--en-us
---my.regex.rx
--pt-br
---my.regex.rx
```
As an example of how to use this, take a look at the [weather skill](https://github.com/MycroftAI/skill-weather).  In the `regex/en-us` folder, there is a `location.rx` file that defines a regular expression for the group `Location`. It looks like this:
```
(at|in) (?P<Location>.*)
```
This can be hard to parse, especially for people who have never seen regular expressions before. Regular expressions are essentially formatted pieces of text that can be used to match a wide range of phrases or strings. 

The chunks of text inside parentheses are called capturing groups, and are used to group similar things. For example, `(at|in)` is a group that will match either the word `at` or the word `in`. The block `(?P<Location>.*)` is more complicated. Like `(at|in)`, it is also a capturing group. However, the `?P<Location>` syntax is used to give a name to whatever it captures, which is very useful for our purposes. In this case, it gives it the name `Location`. The following two characters, `.*`, are what are used to define what this group captures. The dot character, `.` can be used in regex to represent any character except for newlines. The `*` special character is used to repeat something zero or more times. So together, `.*` matches zero or more characters of any kind. This means that the regex `(at|in) (?P<Location>.*)` will match something like `in London`, as well as `at the corner store`. In the first case, the `Location` is London, and in the second, the `Location` is `the corner store`. 

For another example, take a look at the [speak skill](https://github.com/MycroftAI/skill-speak). This is the skill that allows Mycroft to Parrot back what you speak. For example, if you were to say "Hey Mycroft, say I am the very model of a modern major general," Mycroft will respond with "I am the major model of a modern major general." 

Note: While this skill doesn't illustrate a proper example in terms of folder structure, it does allow one to see how the regular expressions interact with the rest of the utterance. 

The line:
```bash
 prefixes = [
            'speak', 'say', 'repeat']
        self.__register_prefixed_regex(prefixes, "(?P<Words>.*)")
```

creates the sentence structure where the regular expression```(?P<Words>.*)``` represents the string elements that will get repeated back and the list of prefixes represent vocabulary words that trigger the skill. 

As an exercise, try to re-write the speak skill by creating the proper folder strcuture. The vocabularly file is going to consist of 
```
speak
say
repeat
```

And the regex file is going to consist of ```(?P<Words>.*)```.

To import these into the ```__init__.py``` file, you will need an intent builder function call similar to the one in the weather skill.
```bash
  intent = IntentBuilder("CurrentWeatherIntent").require(
            "WeatherKeyword").optionally("Location").build()
```

For a guide on the syntax of regular expressions, we recommend the following pages:  
[Regular expression operations (Python documentation)](https://docs.python.org/2/library/re.html)  
[Python Regular Expressions (Google documentation)](https://developers.google.com/edu/python/regular-expressions)