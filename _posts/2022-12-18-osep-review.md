---
title: OSEP Review
author: w33vils
date: 2022-12-18 08:00:00 +0300
categories: [Blog, Reviews]
tags: [OSEP]
pin : true
---

I recently passed the Evasion Techniques and Breaching Defenses course or as it is known - [Offensive Security Experienced Pentester (OSEP)](https://www.offensive-security.com/pen300-osep/) exam by Offensive Security and here are my *no-one-asked* thoughts on the course!

![Active Directory Lab](/assets/img/images/osep_badge.png)

### TLDR

This is by a margin the hardest, yet most satisfying course I have taken. While the 72-hour (Inclusive of 24 hours for reporting) exam is challenging, it is the course, labs and support that you get along the way that's worth its value. It is more about the journey.....

### The Course

OSEP is an advanced penetration testing course that builds on the knowledge gained in [OSCP](https://w33vils.github.io/posts/oscp_review/) to go against a mature organization with modern defenses. The course achieves this by focusing on custom offensive tool development and teaching concepts such as:

- Client-Side Code Execution.
- Process Injection & Migration.
- Antivirus Evasion.
- Application Whitelisting
- Kiosk Breakouts.
- Bypassing network filters.
- Linux Post-Exploitation.
- Linux Lateral Movement.
- Advanced Windows Exploitation.
- Microsoft SQL attacks.
- Active Directory Exploitation.
- etc

Every section covered has a dedicated lab environment where you can practise and cover the exercises and at the end, you get six (at the time of writing) dedicated lab networks where you get to combine all the tradecraft taught in the course to compromise the environment. The course is well thought through and each module builds upon the previous and goes in depth  on every section with the *why's* and *how's*. You can truly tell Offensive Security took their time to create the material and the value gained overall is worth more than the certification paper itself alludes. 

I took roughly three months of intense preparation, but I probably spent more factoring in that I took the [Certified Red Team Professional](https://w33vils.github.io/posts/crtp-review/) course work and exam to help me prepare for this course. Every module in the OSEP course taught me something completely new and in *many* instances felt quite overwhelming. But hey, it is called an **advanced** pentesting for a reason no?

Now I want to insist on the intense preparation bit as most people tend to focus on the carrot and forget the stick that really goes into it. Of course the metaphor is incorrectly used here but you get the picture. Unless you are doing advanced pentesting as your daily job, you are going to spend significant number of hours learning how to code exploits in C#, writing PowerShell scripts, exploring VBA and wondering why some exploit works in the dev machine but not on the challenge machine.

![](/assets/img/images/denzel.gif)
<figcaption align = "center"><i>Exploit completed but no session was created</i></figcaption>

### The Exam

The exam is 48 hours long for the hacking bit and a further 24 hours to submit the report. The exam objective is outlined to you on your exam control panel, but in summary, you either find a secret.txt flag, or attain 100 points to pass. There might be more than one way to get to the desired objective, so don't spend too much time on one thing. If the door doesn't work, try the window. Or knock the entire wall down.

The course itself *should be enough* to pass the exam. Should be, because you will equally need the OSCP knowledge to get through some areas and they do mention this as part of the requirement. So popping a few boxes too as part of your prep won't be too bad.

### My Tips

- It is probably best to learn some C# before starting the course. Much of what you will write will be *similar* to this [Defcon C# workshop](https://github.com/mvelazc0/defcon27_csharp_workshop) so wouldn't hurt to go through it. Going through some YouTube course will go a long way as well. [Can check this one out](https://www.youtube.com/watch?v=GhQdlIFylQ8), but there are probably more.
- Do alot of research around Active Directory Exploitation. While CRTP is not required, I would recommend it. However, you can still find many, many, relevant material online that do the exact same job.
<ul style="margin-left: 60px;">

  <li><a href="https://www.ired.team/offensive-security-experiments/active-directory-kerberos-abuse">https://www.ired.team/offensive-security-experiments/active-directory-kerberos-abuse</a></li>
      <li><a href="https://tryhackme.com/room/exploitingad">https://tryhackme.com/room/exploitingad</a></li>
    <li><a href="https://github.com/S1ckB0y1337/Active-Directory-Exploitation-Cheat-Sheet">https://github.com/S1ckB0y1337/Active-Directory-Exploitation-Cheat-Sheet</a></li>
    <li><a href="https://book.hacktricks.xyz/windows-hardening/active-directory-methodology">https://book.hacktricks.xyz/windows-hardening/active-directory-methodology</a></li>
</ul>

- Bloodhound is not covered in the course, which is a bummer, but, this will make your work easier.
- [adPEAS](https://github.com/61106960/adPEAS)
- Some other useful references:
<ul style="margin-left: 60px;">

  <li><a href="https://github.com/In3x0rabl3/OSEP/blob/main/osep_reference.md">https://github.com/In3x0rabl3/OSEP/blob/main/osep_reference.md</a></li>
      <li><a href="https://casvancooten.com/posts/2020/11/windows-active-directory-exploitation-cheat-sheet-and-command-reference/">https://casvancooten.com/posts/2020/11/windows-active-directory-exploitation-cheat-sheet-and-command-reference/</a></li>
    <li><a href="https://ppn.snovvcrash.rocks/pentest/infrastructure/dbms/mssql">https://ppn.snovvcrash.rocks/pentest/infrastructure/dbms/mssql</a></li>
    <li><a href="https://gist.github.com/TarlogicSecurity/2f221924fef8c14a1d8e29f3cb5c5c4a">https://gist.github.com/TarlogicSecurity/2f221924fef8c14a1d8e29f3cb5c5c4a</a></li>
        <li><a href="https://github.com/Porchetta-Industries/CrackMapExec">https://github.com/Porchetta-Industries/CrackMapExec</a></li>
        <li><a href="https://exploit-me.com/blog/osep-cheat-sheet/">https://exploit-me.com/blog/osep-cheat-sheet/</a></li>

</ul>

- Study to understand, not to complete a module. It is ok to spend a few days on a concept. No one was born a hacker.
- Make good notes, no really, take good notes. If you need to use a command more than once, it should probably be somewhere you can easily copy paste.
- Have confidence in yourself. "Those who believe they can do something and those who believe they can't are both right" ~ *Henry Ford*
- Stream peak Ronaldo goals as you study. :-D


### Finally

This is a really great course! and I am happy that Offsec now have a discord channel where the staff are super helfpul. This is a huge improvement from the Offsec forums where some hints go like "Go dance with Julius". Sometimes you don't know what you don't know, and it is helpful to get that proper push along the right path.

If you are looking to advance your pentesting skills and understand the crust of how to beat modern defenses, this is your course! 

"Very Nice!"

![](/assets/img/images/hacking.gif)
<figcaption align = "center"><i>Meterpreter Session 1 opened ... </i></figcaption>



