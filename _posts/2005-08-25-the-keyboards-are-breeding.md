---
layout: post
title: The keyboards are breeding!
---
On my work desktop I have three machines. “Why three machines” I hear you ask?

1. A Windows Desktop, running the Imperial College Corporate Desktop.
   This is pretty much required equipment nowadays. Our Helldesk software
   (Marval Open Pursuit) only runs on Windows. There is a Web interface,
   but it’s not feature complete, so it’s almost impossible to use on a day
   to day basis. Also, I’ve been running Evolution for ages to connect to
   my Exchange account - this works, but as you delve more into shared
   calendars, permissions, group scheduling and the like, Evolution just
   doesn’t cut it. I’m also more and more working on Linux/Windows
   integration, so I need a test for the other half.
2. An HP xw9300 Workstation, running RedHat Enterprise Linux.
   This is my main desktop and it is pretty much the dog's bollocks -
   dual Opteron 248s and an Nvidia Quattro NVS280 with dual displays.
   It got bought so we could test 64bit architectures for rollout, but
   I’ve kidnapped it for my daily use. I run RHEL4 Workstation on it,
   mainly because that’s my main development focus. In actual fact,
   I’m currently running Fedora Core 4 on it, because I wanted to check
   if all our install scripts could cope with FC4. I’ll move back to RHEL4
   when the next update comes out in a month or two.
3. A iMac Lampshade running OSX 10.4 (Tiger).
   I’m a nominal member of our Mac Development Group, taking care of our
   XServes and I inherited this machine of someone who left. At the moment,
   I use it only for IM (Adium) and iTunes - plus I sometimes use Apple
   Remote Desktop to connect to our servers.

All this leaves me with 3 machines (well two of them are under the desk),
4 monitors, 3 keyboards, 3 mice and a pair of speakers. Plus I’ve got a
phone on my desk too. I was getting annoyed with the huge amount of desktop
dedicated to keyboards and I’m always impressed by those people with 16
monitors all lined up dragging windows all over the place.

In the end I decided that x2vnc looked like an excellent idea - so I
installed it on my workstation which occupies the central two screen slots
on my desk. I then installed OSXvnc on the iMac and RealVNC on the Windows
machine. Setup both VNC servers to start automatically gave both machines
a quick reboot and there we go.

Then I created some scripts to connect the desktops at the click of a button
and put a link on my startbar - now all I have to do is login to my Workstation,
click a button and with one keyboard and mouse I can navigate across 3
computers and 4 screens… excellent!

vncconnect:

```sh
#!/bin/bash
EXIT=1
while [ $EXIT != 0 ]; do
 x2vnc -passwdfile ~/.vncpass -west ccsjslin:0 2>&1 >/dev/null
 EXIT=$?
done
```

vncconnect2:

```bash
#!/bin/bash
EXIT=1
while [ $EXIT != 0 ]; do
 x2vnc -passwdfile ~/.vncpass -east ccsjsmac:0 2>&1 >/dev/null
 EXIT=$?
done
```

condesk:

```bash
#!/bin/bash
~/.bin/vncconnect&
~/.bin/vncconnect2&
```

Magic innit?
