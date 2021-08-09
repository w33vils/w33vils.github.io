---
title: Python DowntimeDetector
author: w33vils
date: 2020-08-23 08:00:00 +0300
categories: [Blog, Scripts]
tags: [python, downtime, telegram, regex]
---

## What it is ...

Earlier on I wrote about how I wanted to get high severity notifications about  a particular critical system on my Telegram channel. That was pushed by desire of not having work emails enabled on my mobile device, but also not miss on critical system alerts, that are usually shared via mail by the system. 
You can read about it under the [Python - emailBot](/posts/blog_emailbot.md) section and the code [here](https://github.com/w33vils/emailBot).

A flaw in the project is that, in the event the entire system goes offline, it would not send any alerts that I would then capture from the emails. I needed a different way to monitor the host itself, independently from itself. Sure, there are many (and perhaps more efficient) ways to achieve this, but I wanted to play around and do it via a customized script. A way to learn the language too.

## Tasks

On a high level, I needed a script that would:

- Can monitor a system's uptime
- Send an alert to my Telegram channel in the event of a failure
- Provide continuos monitoring after the fact
- Monitor multiple hosts at the same time

So, what do you do when you have a coding problem?

![](https://media.giphy.com/media/eBD5RhS0n5JgA/giphy.gif)

## Code

### Continuos monitoring

I found an interesting `python` module - [multiping](https://github.com/romana/multi-ping) which allows you to monitor multiple hosts using ping requests. The module works by sending multiple retries within a defined timeout period to a set of hosts and records which ones are online or offline. A test of the module runs as below:

```python
from multiping import multi_ping

addrs = ["8.8.8.8", "youtube.com", "192.168.50.100"]

# Ping the addresses up to 4 times (initial ping + 3 retries), over the
# course of 2 seconds. This means that for those addresses that do not
# respond another ping will be sent every 0.5 seconds.
responses, no_responses = multi_ping(addrs, timeout=2, retry=3)

print("Responses : %s" % list(responses.keys()) + "\n"
      "No Responses : " +str (no_responses))
```
From which you get a similar result to the one below:

```
Responses : ['8.8.8.8', '216.58.223.78'] 
No Responses : ['192.168.50.100']
```

From here, it gets simple. We just loop through the code and then send an alert anytime there is a downtime and another alert when the host comes back online.

### Timestamp

Before doing that, we need functions to check the timestamp, another to calculate the time difference and the last one to send the telegram message.

The code gets us the current time.

```python
def current_timestamp():
    return datetime.datetime.now()
```

While the python method piece below gets the time difference:

```python
def time_difference(start, end):
    difference = end - start
    secs = str(difference.total_seconds())
    return str(datetime.timedelta(seconds=float(secs))).split(("."))[0]
```

We will constantly call this method to get the timestamp when needed, (e.g., when we want to know for how long the host has been offline.)

### Telegram Messages
To send messages to Telegram, we need a `bot` and a `channel`. The bot needs to be an administrator on the channel. [Create a Bot with BotFather](https://core.telegram.org/bots#:~:text=for%20existing%20ones.-,Creating%20a%20new%20bot,mentions%20and%20t.me%20links.) and note the `bot token`. Then create a public channel and add the bot as an administrator.

To get the channel ID (which we will use as the chat ID),  post the URL below on your browser, replacing the `bot_token` with your bot token.

```plaintext
https://api.telegram.org/bot<bot_token>/getupdates
```
Then post a random message on the channel and reload the link.  You will see the chat ID as

 `"chat":{"id":-xxxxxxxxxxx, ...`

  The Telegram function below  takes the message and uses a telegram bot token, to send a message to the telegram channel or chat.

  ```python
  def botsy(token, chat_id, telegram_message):
    bot = telegram.Bot(token)
    bot.sendMessage(chat_id=chat_id, text=telegram_message)
```


### Finally

We need to continously monitor the system for uptime and downtimes. For this, we can implement a simple while loop as below.

```python
while True: #loop through the check host function
    if check_host(addrs):
        continue
    else:
        down_time = current_timestamp()
        message = "☒ Host " +str(addrs[0])+ " is down as at " + str(down_time).split(".")[0]
        botsy(token, chat_id, message)
        counter = 0
        while not check_host(addrs):
            counter += 1
            current_time = current_timestamp()
            message = "☒" + str(addrs[0]) + " Has been down for " + time_difference(down_time,
                                                                                      current_time) + " HH:MM:SS"
            if counter == 600:
                botsy(token, chat_id, message)
            if counter == 30: #3600
                botsy(token, chat_id, message)
            if counter == 45: #10800
                botsy(token, chat_id, message)
            if counter == 60: #21600
                message = "☒ Host\n" +str(addrs[0]) + " has been down for over an hour. No more alerts will be sent. "
                botsy(token, chat_id, message)
                continue

        up_time = current_timestamp() #Get restoration time
        message = "✅ Host " + str(addrs[0]) + " is now up after " + time_difference(down_time, up_time) + " HH:MM:SS"
        botsy(token, chat_id, message)
```
The loop  continuously checks the `check_host` function, if the provided address is up, it does nothing. If it is down, it picks the current downtime from the `check_downtime` method, and sends it to Telegram via the bot. 

We then use a basic counter to split our reminders. In this case, if a host is not up after ten minutes, a reminder will be sent after 10 minutes, then after 30 minutes and finally after one hour, after which no further alerts are sent. 

This helps with alert fatigue, Plus, if it's still offline after one hour, it probably wasn't too important for you, was it?

## Improvements

- The obvious issue with the code is that, while `multiping` module has the capability to ping multiple hosts, my humble code has not achieved this. So far, it can only ping one host at a time. 

Theoretically, this can be fixed by implementing a database of the hosts and and their states at any time and reading and updating as they come up or go down. This can also be done by updating an excel sheet, but a database would certainly make you look smarter.

I will be looking to update this post once I fix the issues, but for now you can find the full code to monitor the single host using ping, with Telegram notification, on my [Github page](https://github.com/w33vils/downtimeDetector)