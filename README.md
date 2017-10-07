
## Features

### Checkin in

**Scenario: @snookbot checks in with you**
Given it's a working day
When you log into Slack
And this is the first time you've stayed active for more than 15 minutes today
Then @snookbot will check in with you


**Scenario: You check in with @snookbot**
Given you want to update your status
When you @mention snookbot and say "Just checking in" or use the work "checking in"
Then @snookbot will run the checkin script


**Scenario: The end of the day**
Given its the end of the day
Then @snookbot will clear all statuses and set up for the next day


**Scenario: You havn't checked in today (you're on holiday or not logged in)**
Given you havn't checked in today
Then @snookbot won't store any data for you


**Scenario: Finding out who is interruptable today**
Given you want to find out who is interruptable
When you @mention snookbot and ask "Who is interruptable today?"
Then @snookbot will send you a list of who is interruptable and when.

"Looks like:"

**Lili** is **This Morning**
**Mat** is **This Afternoon**
**Izzy** is **All Day**


**Scenario: Finding out who is interruptable right now**
Given you want to find out who is interruptable right now for a call
When you @mention snookbot and ask "Who is interruptable now?"
Then @snookbot will send you a list of people who are active
And whose interruptable status matches the current time of day.

Example reponse: **Mat** and **Victoria** are interruptable right now.


**Scenario: Getting a Snook weather report**
Given you want to get a weather report for the mood in Snook
When you ask @snookbot "What's the weather like today?"
Then @snookbot will see how people are feeling and prepare a weather report.

Example weather reports:

"It's going to be a sunny, sunny day",
"Looks like a warm day"
"Cloudy with a chance of rain",
"Generally sunny but there might be a few stormy clouds"

I have questions here, maybe this isn't appropriate...we don't want to stigmatise people who.
I suppose with the analogy, the weather is the weather,


**Scenario: Getting a weather report by studio**
Given you want to get a weather report for the mood in a Snook studio
When you ask @snookbot "What's the weather like in {location}?"
Then @snookbot will see how people are feeling and prepare a weather report.

Example weather reports:

Example weather reports:
"It's going to be a sunny, sunny day",
"Cloudy with a chance of rain",
"It might be a little stormy later"


#### Snookbot checkin script

```
Question 1: "{ Morning | Afternoon | Howdy | Other random greetings } {name}, how are you feeling?"
Options (pick an emoji response): {
    "sunny" : 🌞,
    "cloudy": 🌥,
    "rainy": 🌧,
    "stormy": ⛈
}

If you choose rainy or stormy, then @snookbot will private message your snook buddy.

    "Looks like {name} is having a { rainy | stormy } day today, maybe check the weather with them in an hour or so? Perhaps its just a shower."

Question 2: "Are you interruptable this morning?"
Options: { Yes | No }

Question 3:"Are you interruptable this afternoon?"
Options: { Yes | No }

This will output: { This morning | In the afternoon | All day (if both yes)| Not today (if both no) }

Option 4: "What are you thinking about today?"
Options: What ever you want.
```