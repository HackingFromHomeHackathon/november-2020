
# Head Coach
Joe Leveridge's submission for Mattermost Hackfest 2020.
## Problem Statement
In a recent study on mental health by [Accenture](https://www.accenture.com/_acnmedia/pdf-90/accenture-tch-its-all-of-us-research-updated-report.pdf), sixty six percent of the employees who participated in the survey reported having personally experienced mental health challenges. Eighty five percent said someone close to them had experienced a mental health challenge.

Today we have a much better understanding about how Mental Health varies on a spectrum from good to bad and how it differs from person to person and from time to time.

However, despite considerable progress in the field, it’s still hard to talk about our mental health at work.

> Ninety percent of workers have been touched by mental health challenges, either personally or through someone they are close to

Furthermore, if that was hard enough, we are now amidst a global pandemic with many workers forced into isolation and a work from home posture. Employees are worried, anxious and frustrated and have had their normal support systems stripped away.

We need more tools to help people feel safe about raising concerns about their emotional wellbeing and to not feel they need to hide how they are feeling.

## Underlying Use Cases
Introducing your brand new 'Head Coach' bot. The Head Coach plugin helps you to regularly take a moment to reflect on how you are feeling.

The Mattermost 'Head Coach' will send you a daily reminder message to rate "How is your emotional health today?" through a simple UI. You can also make a note of any specific factors that are contributing to your current mental state.

Head Coach will acknowledge your submission and provide guidance on you can either improve your mental state or share your energy with others.

### Approach
As a complete beginner, my first two days involved setting up my developer environment (Mac Docker) and completing a 'Go Fundamentals' course on Pluralsight.

I then brainstormed some ideas and made some initial sketches on paper. I then made a list of requirements for my bot that included:

- Daily message asking to score their emotional health
- Voting buttons on sidebar UI to rate emotional health
- TextArea on sidebar UI to provide reasons behind their emotional state
- Share button to submit the score
- Set of feedback/guidance messages to be delivered as a response
- Ability to check what the previous score was

Next I created a new repo based on the Mattermost sample template and reviewed / butchered some existing plugins that had similar features.

I then set about creating my bot based off the existing plugins (Welcomebot/To Do/Demo Plugin) -- thanks to all those who worked on these!

### Screenshots
#### Main View
Icon showing doctor with stethoscope in header menu opens sidebar view.

![Plugin View](https://github.com/jl386/mattermost-plugin-mhbot/blob/master/screenshots/Rate_Score.png?raw=true)

The emotion is highlighted once it has been clicked. User can type an optional note in the notes field and submit by clicking the share button.

![Plugin View Selected Option](https://github.com/jl386/mattermost-plugin-mhbot/blob/master/screenshots/Rate_Score3.png?raw=true)

After your first submission, your last rating will be shown at the top of the bar.

![enter image description here](https://github.com/jl386/mattermost-plugin-mhbot/blob/master/screenshots/Rate_Score2.png?raw=true)

#### Information (Help) Modal
If you click the Help icon you are presented with further information about the bot.

![Information Modal](https://github.com/jl386/mattermost-plugin-mhbot/blob/master/screenshots/Info_Modal.png?raw=true)

#### Score Guidance
Once you have shared your rating, the bot acknowledges your submission and provides some guidance based on your rating.

|Excellent|Good|Average|Poor|Terrible|
|--|--|--|--|--|
| ![Excellent Feedback](https://github.com/jl386/mattermost-plugin-mhbot/blob/master/screenshots/Feedback_Excellent.png?raw=true) | ![Good Feedback](https://github.com/jl386/mattermost-plugin-mhbot/blob/master/screenshots/Feedback_Good.png?raw=true) | ![Average Feedback](https://github.com/jl386/mattermost-plugin-mhbot/blob/master/screenshots/Feedback_Average.png?raw=true) | ![Poor Feedback](https://github.com/jl386/mattermost-plugin-mhbot/blob/master/screenshots/Feedback_Poor.png?raw=true) |![Terrible Feedback](https://github.com/jl386/mattermost-plugin-mhbot/blob/master/screenshots/Feedback_Terrible.png?raw=true)

### Demo
Please see link to a short video summarising the problem statement and showing the working prototype:
  [Summary Video and Prototype Demo](https://biteable.com/watch/hackathon-2020-2728140)

### Source Code
Link to the source code:
https://github.com/jl386/mattermost-plugin-mhbot

### Reflection
I have learnt _so_ much this past week pulling/hacking apart these projects and putting them back together based on my idea. I wasted a serious amount of time in React/Redux which at times was infuriating (also did some Redux tutorials!) However I am super proud of participating in my first Hackathon and that I have produced something that works!

## To Do
This is just the beginning! Some of the features I wanted to look at but ran out of time include:

-  **Trends** (Ability to view your last X scores and notes on a chart)

-  **Trend Analysis** (Head Coach bot to notice when you take a leap or a dip, send a congratulatory GIF when you move from good->excellent, or send further guidance when you fall from average->poor).

-  **Circle of Trust** (Configure your closely trusted private circle to which you automatically share your scores/trends. Friends can be notified to reach out when you are feeling low)

-  **Mental Health First Aid** (Head Coach connects you to an available mental health first aider.)

	- Mattermost: Automatically create the direct channel. Through sidebar, provide the first aider with conversation starters which can be automatically posted on their behalf when clicked)

	- Jitsi: Automatically kick-off a video call with your designated first aider or member of circle of trust
