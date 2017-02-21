---
layout: post
title: Waking Up to A Livestream
tags: [mac, python, tutorial]
---

Recently there was a post on imgur listing some [24/7 music streaming stations](http://imgur.com/gallery/puU0r). I found the music to be quite relaxing and thought that I would love to wake up to new music like this everyday.

So I decided to look into a way to automatically launch the livestream URL at a specified time every day. This led me to look more deeply into a concept I had heard about called cron jobs. I found an [article](https://ole.michelsen.dk/blog/schedule-jobs-with-crontab-on-mac-osx.html) describing the process of using a crontab, which I will paraphrase below.

To add a job to crontab you need to edit the job list. A job is created using the following format: 
```
* * * * *  command to execute
     │ │ │ │ │
     │ │ │ │ └─── day of week (0 - 6) (0 to 6 are Sunday to Saturday, or use names; 7 is Sunday, the same as 0)
     │ │ │ └──────── month (1 - 12)
     │ │ └───────────── day of month (1 - 31)
     │ └────────────────── hour (0 - 23)
     └─────────────────────── min (0 - 59)
```

To open the URL programmatically I used the below script named urlopener.py, which is run through Python 2.7.6.

```
#!/usr/bin/python
import webbrowser

url = "https://www.youtube.com/c/chilledcow/live"

webbrowser.open(url, new=0, autoraise=True)

```

To edit the job list I used the nano editor.
```
env EDITOR=nano crontab -e
```

To have the URL open every day at 6:45AM I entered the following.
```
45 6 * * * /Users/user/urlopener.py
```
To correctly execute the script each day I provided the script's full path, which is easily obtained by dragging the script from Finder into Terminal.
After entering the above, save and exit the editor by using <kbd>control</kbd> + <kbd>o</kbd> and <kbd>control</kbd> + <kbd>x</kbd>.

To verify that the crontab job has been added use the following command:
```
crontab -l
```
I hope this exposes some to the utility of cron jobs and the power of python scripts. I am certainly enjoying my new alarm!