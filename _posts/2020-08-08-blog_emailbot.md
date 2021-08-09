---
title: Python emailBot
author: w33vils
date: 2020-08-21 08:00:00 +0300
categories: [Blog, Scripts]
tags: [python, email, telegram, regex]
---

# Email - Telegram Python Bot

As a a cyber security architect, I am often responsible for some critical security infrastructure, whose uptime is, well, you guessed it, paramount. Usually, these systems have some sort of warning bells when hell breaks loose, and this can be in the form of email alerts, or monitoring dashboards.

I wrote this script to avoid checking emails on weekends. You probably also, don't want to go back to work on Monday, to find your infrastructure went off on Friday evening, and no one was there to give it CPR.

![](https://media.giphy.com/media/26AHLsZkEKRGMFgFq/giphy.gif)

Since I am always on my phone, I wanted an easier, less stressful way to receive high priority alerts.

## Problem Statement

I was responsible for a system that generated such email alerts as below, sometimes in thousands:

```
Event Type: Gateway state change
Time: 8/4/20 11:04 PM
Subsystem: Gateway
Severity: High
Message: The status of the gateway SERVER1-GW-01 is Disconnected. Please check the gateways section of the user interface for additional information.
Reporting Component Name: SERVER1-GW-01
Reporting Component IP: X.X.X.X
```
I wanted to filter from the thousands of similar alerts, get the Critical severity ones (usually pointing to a downtime) in a stripped-down format, sent to my phone.

## Pseudo-Code
  - Scan an email folder for unread emails

  - Parse the emails and extract the content

  - Find the most important parts of the message
  
  - Send the information as a Telegram alert

  I found a fantastic blog on [repl](https://repl.it/talk/learn/How-to-Make-a-Python-Email-Bot/8194) which helped me quickly cover some bits of the task.

## Code

The complete code is available on my [Github Page](https://github.com/w33vils/emailBot). I have explained the important bits below.

- ### Connecting to the email Server


In this code, I will be using Outlook as the email server. We will use the `imapclient python` library to connect to the outlook server. The imapclient library implements a method that takes the *username* and *email* and connects to the email server.

```python
        print("Initializing IMAP ... ", end="")
        global connect
        connect = imapclient.IMAPClient(imap_server)
        connect.login(read_from, password)
        connect.select_folder("INBOX", readonly=False)
        print("Success")
```
`readonly=False` ensures the emails are marked as read. This avoids duplicates.

- ### Reading emails

Unread emails are returned as `UIDs`. The UIDs are what we use to fetch actual emails.

```python
//Code that checks for unread emails

uids=i.search(['UNSEEN'])
if not uids:
    return None
else:
    print("Found %s unread emails" %len(uids))
    return i.fetch(uids, ['BODY[]', 'FLAGS'])
```

Next we analyze and return the actual message. `pyzmail` module can help us extract the sender, subject, and message. It is important to only analyze messages from the particular sender, to avoid another system or user sending a conflicting email. Also, since I am only interested in the high severity events, I will ignore any emails with a medium or low severity in the subject.

```python
message=pyzmail.PyzMessage.factory(raws[a][b'BODY[]'])
global subject
subject=msg.get_subject()
from=msg.get_address('from')
if frm[1] != sender_address:
    print("Unread is from %s <%s> skipping" %(frm[0][0], frm[0][1]))
    return None
if msg.text_part is None:
    print("No message to parse")
    return None
if "High Severity" not in subject:
    return None
```

- ### Extract the important parts from the message
Using regex, we can analyze the message returned and extract the information, from the data.

The targeted piece is:
```plaintext
Message: The status of the gateway SERVER1-GW-01 is Disconnected. Please check the gateways section of the user interface for additional information.
```
For a telegram message, we can send `SERVER1-GW-01 is Disconnected`, which is short, and most importantly sweet.

The regex code below does just that.

```python
def get_event(raw_msg):
    pattern = re.compile(r'(\bMessage:)([a-zA-Z0-9-\s]+(\bgateway)([a-zA-Z0-9-\s]+.))', re.I)
    matches = pattern.finditer(raw_msg)
    return matches
```
- ### Sending the message to Telegram

To send messages to Telegram, we need a `bot` and a `channel`. The bot needs to be an administrator on the channel. [Create a Bot with BotFather](https://core.telegram.org/bots#:~:text=for%20existing%20ones.-,Creating%20a%20new%20bot,mentions%20and%20t.me%20links.) and note the `bot token`. Then create a public channel and add the bot as an administrator.

To get the channel ID (which we will use as the chat ID),  post the URL below on your browser, replacing the `bot_token` with your bot token.

```plaintext
https://api.telegram.org/bot<bot_token>/getupdates
```
Then post a random message on the channel and reload the link.  You will see the chat ID as

 `"chat":{"id":-xxxxxxxxxxx, ...`

 We can then we use the `sendMessage` method to send the alert to Telegram.

 ```python
 def botsy(bot_token, chat_id, telegram_message):
    bot = telegram.Bot(bot_token)
    bot.sendMessage(chat_ID, text=telegram_message)
```

- ### Finally

Finally, we loop through methods created to monitor for new emails, analyze them, pass them through a regex function to get the required message and send it to Telegram. Then keep waiting for new messages/alerts to arrive.

```python
while True:
    try:
        messages=get_unread()
        while messages is None:
            time.sleep(check_freq)
            messages = get_unread()
        for a in messages.keys():
            if type(a) is not int:
                continue
            received_email=analyze_msg(messages, a)
            if received_email is None:
                pass
            elif received_email:
                parsed_email = get_event(received_email)
                for match in parsed_email:
                    if not match.group(4):
                        # print(match.group(4))
                        pass
                    elif match.group(4):
                        botsy(str(match.group(4)))
                        break
                    else:
                        pass
```
The loop checks for any unread messages and checks whether the sender is from the system we want to monitor. If there are no messages, it sleeps for a defined time interval and rechecks.
If a message is received, it is analyzed, and the body part extracted which is then checked by the regex function to determine if it contains the required message that warrants a notification on Telegram. If such an alert exists, it is sent Telegram. 
The `match.group` only checks the fourth item returned from the regex function, since it is the important bit that we care for. This area requires customization to suit your own needs.

- ### One more thing

We create a config file to carry the different variables defined on the code. Which is then imported to the code.

The code gets the mailbox to read emails from and its associated `imap` server, the password using the `getpass` library which will hide the password when it's being typed.

```python
import getpass

read_from=input("Enter mailbox to read from: ")
imap_server=input("Enter imap server: ")

paswd=getpass.getpass("Account Password: ")
sender_address =input("Enter the trusted system email sender address: ")

bot_token = input("bot token : ")
chat_ID = input ("chat id : ")
```
- ## Results

When one of the servers experiences a fault and goes offline, we get a server disconnected alert on telegram and when it gets online, an uptime alert is sent.

![](/assets/results.png)
_Notifications sent to Telegram_

That's it!
