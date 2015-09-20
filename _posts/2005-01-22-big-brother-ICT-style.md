---
layout: post
title: Big Brother, ICT Style
---
There's a big push here at work to maintain central records of all our machines. The fact we have
umpteen thousand, mostly purchased individually to a variety of specifications from a variety of
grants by a plethora of Academics, makes it very hard indeed

We insist that Windows machines are part of our active directory infrastructure and part of that
is a policy to regularly run Everest, a hardware/software auditing program. This data is linked
up with other available information to provide a complete picture of machines connected to our
network - as long as they are running Windows.

I did a bit of work last week (don't faint from shock) taking a small perl script written by one
department for Mac OSX 10.3 and extending it to compile simple audit information for any version
of OSX and log it to a central windows share. Unlike Windows we don't automate the running of this
script, because we don't have a centralised Mac infrastructure - Yet

In contrast, we do have a somewhat centralised Linux infrastructure and it's my baby. So I've
spent a little time thinking about the problem of maintaining a complete machine database and
come up with the following ideas:

1. Use RedHat’s up2date hardware collection libraries.
2. Use lshw and a small perl script.

I settled on [2] because up2date is written in Python, an evil language. Once I'd found that
lshw outputs some nicely formed XML, I simply took some perl and glued together the lshw hardware
output with an XML representation of the RPM database and some basic user stats. I'm then checking
a webpage for the location of the audit upload page and uploading a file to that page.

This approach leaves me with three things:

1. a local copy of the audit output
2. webserver logs listing who is asking about the audit script
3. a server copy of the audit output to process

So now I just have to work on further storage and processing of the audit. For this I will be using
PHP5 and its SimpleXML methods and extensions, because that is an easy method of turning XML into
a PHP object. I'll probably be placing this all in a database as well.

And this is all just as a side-project… I have a real job to do.
