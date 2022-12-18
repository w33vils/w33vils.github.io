---
title: My OSCP Experience
author: w33vils
date: 2021-07-31 08:00:00 +0300
categories: [Blog, Reviews]
tags: [OSCP]

---

I recently passed the Offensive Security Certified Professional (OSCP) exam, and as is a rite of passage, I will shamelessly add to the already existing, hundreds of reviews!

If you are reading this, you are probably preparing or thinking of enrolling for the OSCP course. You may also just be here to read my blog, either case, rock on!

### TLDR

I passed on my second attempt after failing narrowly on my first. My take? The exam is completely doable and while the preparation can be taxing depending on your experience level, it really **isn't** the worst exam on earth. You can do it.

> Completed:

    - Completed THM Offensive pentesting path, and some more rooms - 70+ in total.
    - 59 boxes on HTB
    - All 75 (at the time) PWK labs
    - Approximately 50 boxes on PG Practice 

## How It started

I decided to enroll for the OSCP purely out of the need to improve my hands-on skills on hacking, Linux and Active Directory pentesting, although the latter isn't extensively covered in the course. Safe to say, after getting my CEH, I did not quite feel like a hacker:-) .

### Background

I had slightly over two years (at the time) experience as a Cyber Security Architect, but not so much on the CTF or Penetration Testing side of things. For all intents, I was approaching OSCP as a complete beginner.

## Preparation

I first enrolled for The Cyber Mentor's [Practical Ethical Hacking](https://www.udemy.com/course/practical-ethical-hacking/) course on Udemy, which I would 100% recommend for any beginner. The course covers pretty much everything you need for OSCP pre-requisites, from Introduction to Python programming, to basic AD setup and pentesting and the hacking methodology, which is what OSCP is all about.

Next I followed the [Buffer Overflow Made Easy](https://youtu.be/qSnPayW6F7U) series, also from the Cyber Mentor on YouTube, which provides important nuggets in case Buffer Overflows are a new concept to you.

Then I enrolled on the Offensive Pentesting path on Try Hack Me, where I did all the rooms, 25 at the time in about one month. I would also recommend doing this path, in case you are a complete beginner. It will introduce you to different scenarios which are extremely important down the road.

After the one month on THM, I enrolled for Hack the Box and was more focused on following the [OSCP Like List of boxes](https://docs.google.com/spreadsheets/u/1/d/1dwSMIAPIam0PuRBkCiDI88pU3yzrqqHkDtBngUHNCw8/htmlview#). I did a significant number of these, but not all, plus the list is constantly updated with newer machines. In total I pwned 59 systems on HTB before completing my OSCP. HTB has a CTF feel to it, which the OSCP exam isn't, so be prepared for rabbit holes in the exam, which aren't really there in HTB, or on the least, not as much.

After HTB,  I started my OSCP labs in January 2021, where I pwned all 70 (and 5 more retired boxes) boxes at the time, in about two months, doing and documenting all the exercises in the process (the 5 points can be crucial). I was planning to do my exam end of April, so since I had a month left, I decided to enroll to [Proving Ground Practice](https://portal.offensive-security.com/sign-up/pg) where I did all the boxes, 50 or so at the time. 

In total I did over 180 boxes, which is typically on the higher side, but hey, gotta do what you gotta do.

Finally, I enrolled for my exam in late April, and spent the last week or so watching `ippsec` videos on YouTube (highly recommend).

## Exam

### First attempt

My first exam attempt was a roller-coaster of emotions, from anxiety, to excitement to near tears. I enrolled for a 5AM start time since it coincides to the time I wake up. Due to the anxiety though, I barely slept the night before (big mistake). I started off with the Buffer Overflow box as my scans ran in the background. I completed the Buffer overflow within 40 minutes, including all necessary screenshots.

Next, I tackled the 25-pointer box whilst my mind was still fresh. After close to an hour, I had user, took a short break, and then spent 3 hours getting root. In retrospect, I had seen the privilege escalation route in about the first ten minutes of enumerating, but I spent a big chunk of time overthinking.

With 50 Points in the bag within 5 and half or so hours, I took a longer break to get some breakfast and sun. I was feeling confident at this point, just 20 more points!

I resumed almost 45 minutes later and decided to hit the 10 point box. This box can be tricky, and should not be under-estimated, but I managed to root it in under 10 minutes. I decided to celebrate the win with another twenty-minute break.

After my break, I had well over 16 hours left to get just 10 points (actually just needed 5 since I had documented my lab exercises and that comes with 5 points) from the two remaining 20-point boxes, and that's when the OSCP gods decided it was not my day. I enumerated everything, poked all ports more than four times each, took breaks, took a small walk, I basically did everything I read in other walkthroughs, but 15 or so hours later, I decided to go to bed. I requested the proctor to close my session with about 45 minutes to go.

We live to fight another day.

### Attempt two

With over 180 boxes completed, I did not feel there was much to improve on in terms of my methodology. My scans, even days later did not reveal anything new I would have done.

Fortunately, Offensive Security retired 5 machines after the three weeks of my first attempt, and one of the boxes I had in the exam was part of the 5. I was desperate to know where I went wrong so I had a 15-day lab subscription and I hit the labs once more.

I still struggled with the box for over a day, before realizing I was approaching it with the same mindset I did during the exam. I decided to change my tactics, change my tools, wordlists and scan speeds. It is only then that I realized my scans had missed a critical yet simple item that completely unraveled the entire box. From there I had root within the hour. With renewed confidence, I paid and enrolled for the second attempt, less than 48 away without batting an eye.

### Exam
The second attempt was slightly tougher than the first in my opinion. I spent less time on the BOF, taking 20 minutes this time round, but spent close to three hours to get user on the 25-point box. After taking a short break, I spent another one and half hours trying to escalate privileges to no avail. I took another break and then switched to one of the 20-point boxes. After about two hours, I had user. I took another break, and spent it talking about random things with a friend, which greatly helped reduce my anxiety. After the break, I spent about one hour to escalate privileges on the 20-point box, and with increased confidence, went back to the 25-point box and equally escalated privileges, getting 70 points in about 10 hours. I took a longer break, and took a walk to clear my mind. 

Cam back and spent about 30 minutes pwning the 10 point box. This again was more challenging that the one I had in my first attempt. With 11 hours to go, I wouldn't make much progress on the remaining 20 point box. I managed to get both local and proof flags, but without an interactive shell, which accounts for 0 points when assessed. Decided to sleep for about 4 hours, and then retry, but ultimately, I had to bow out with the potential 80 points and 5 extra from the lab report.

I received my passing email about 48 hours later.

## What worked

- Prayers. 

- PG practice is worth its weight in gold. The platform itself is buggy and feels like it was hurriedly done, but the boxes themselves are worth going through before doing the exam. Consider doing the medium and easy boxes as they sort of reflect what you will find in the exam. While some *easy* rated boxes by Offsec are rated hard or very hard by the community, I would advise you take the Offsec rating, after all, they set the exam.

- Scheduling the exam to coincide with my normal waking up hours certainly helped my body. Consider doing the hard boxes while your brain is still fresh.

- The [Buffer Overflow](https://tryhackme.com/room/bufferoverflowprep) room by Tib3rius in Try Hack me is criminally underrated. Really, do this room and buffer overflow will be a piece of cake.

- The Offsec Prep discord channel was quite useful. Reading success stories and getting encouraged certainly helped. The reddit section for OSCP is equally useful in sharing and learning from different experiences.

- ippsec Youtube videos are super helpful in building your methodology and learning different tricks. Don't ignore them. Also [Rana Khalil](https://ranakhalil101.medium.com/)'s walkthroughs were my go to guides for all boxes I solved or was not able to solve.

- Taking walks, resting, talking to someone, working out, whatever to get your mind off the exam.

- From my first attempt, in as much as I knew I was going to fail, I decided to do the report and submit it. This made report writing an easy exercise the second time round.

## What did not work

- Not getting enough sleep before both attempts certainly was a bummer. The exam experience itself is much of a lesson as is the course, I guess.

- Working full time while working on OSCP can be draining to say the least. My body was crumbling down every so often. They say, give your body some rest, or it will do it for you. There are far greater things than passing OSCP. Don't ignore those things, don't be like me.

- Overthinking. Always try the simple things. The exam is meant to be passed.

- Putting too much trust on tools. Try different tools, different wordlists, don't rely on one. Where possible try manual methods too.

- 'Try Harder', 'enumerate more', it's about time these terms were retired. Sometimes you don't know what you don't know, and "trying harder" isn't the solution.

## Advice

You got this.


![](/assets/img/images/cat.gif)