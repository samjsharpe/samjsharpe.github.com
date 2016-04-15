---
layout: post
title: Why I left GDS
---
In which I explain the many and varied reasons why I decided that my life would
be happier outside of the Government Digital Service after 3+ years service.

## 0. Why I don't hate GDS

This is definitely the first and probably the last time I will ever explain
publicly why I chose to leave a job. I left the Government Digital Service in
August 2015 and I've had few people ask why. It's been long enough that I would
hope any lingering unreasonable dissatisfaction would have dissipated and for
the most part I was happy with the experience and would encourage anyone to do a
tour of a few years helping out the Civil Service.

However, as with anyone leaving an organisation, I did it because I believed I
would be happier somewhere else. That sounds negative, but in reality not every
organisation is for everyone for all time. It's OK to move on, so while this
post is from a guy who chose to move, I hope it's not taken as a criticism of
many former colleagues or in fact a disincentive to join GDS.

I believe the idea of GDS is sound. The UK Civil Service has suffered in many
areas, over many decades, from the belief that specialism is something to be
contracted out in the vain hope that private industry will supply the skills and
knowledge needed and act in the best interests of the Country. That's laudable,
but quite frankly bollocks. (TRIGGER WARNING: I might swear again, sorry mum)

Private industry exists to make money. Pretty much the only benefit it brings to
anyone working in the Civil Service is the outsourcing of risk. In-sourcing
expertise is a great idea and I hope that the UK Civil Service continues to
build and maintain in-house specialist knowledge and capability. I also hope
they do it by adopting skills and methodology that is known to work elsewhere,
so that they maximise the opportunities for people to enter and leave the
service.

## 1. Background - What I did for GDS

I used to be a "Web Operations" for GDS. That title is probably the worst
thought job title anyone has ever created. It's vaguely describes a practice
area within the more general field of systems engineering or administration, but
when you try to apply that to a person, it's an ineffective job title, rubbish
description of what they do and leads to awful phrases like "I need a WebOps".

I was technically employee number 2 in the Web Operations Team on GOV.UK,
starting a few days before Carl Massa, with a decade of system administration 
experience, some exposure to "Cloud", but not much practical experience of 
Configuration Management (puppet) - but we managed to get by, we deployed a 
thing called GOV.UK with the help of some talented consultants and friends.

After a couple of years, I needed something different so I helped out with the 
ill-fated Rural Payment Agency project, where we tried to digitize the process
of applying for subsidies by farmers (historically not particularly digital
people). I think enough has been written about that project that I won't bore
you, but without exception the people were great, the aim was high, it just
lacked a little on the execution side and scope creep killed it.

When GDS disengaged from that project, I then started on the Alpha of GOV.UK Pay
which was fantastic, as I was a team of one, we were going to deploy on AWS and 
I could choose all the tooling, so I got a chance to use Ansible. Lovely team,
great project, but by that time my heart wasn't in it any more.

## 2. The startup culture

The "startup culture" under which GDS operates is pretty punishing. There is
always something that needs to be done and ofter refactoring was secondary to 
new features. Bad choices were made for reasons of expediency and never
revisited, because there was always a new feature needed.

I also don't like some features which are seen as mandatory in some Agile
circles (I don't believe the Agile manifesto mandates them)

 - I hate hotdesking, because you are never comfortable
 - I hate bench-style rows of desks, because they don't let you get comfortable
 - I don't particularly like pairing, because many of the problems I work on
   require thought first, not discussion
 - I really don't like standups. Sharing, talking, unblocking are brilliant, but
   forcing it at a particular time each morning doesn't work.

The "features is everything" culture lead to a complex and bloated system that
was poorly executed. I have never worked on any project that maintained two
separate database technologies (MySQL, PostgreSQL) for so long in parallel. This
of course doesn't include the MongoDB, Redis, Memcache, RabbitMQ instances, all
of which have overlapping feature sets.

I'm a big fan of [Dan McKinley's "Choose Boring Technology" article](http://mcfunley.com/choose-boring-technology)
and in it he discusses the merits of "optimizing globally" - if you can make do
with a technology you have, even if the alternative is better in some way you 
should - and if you absolutely have to swap, you should do it quickly, cleanly 
and globally. We didn't.

## 3. Pay and progression in the Civil Service sucks

Promotion and Pay progression really really sucks in the Civil Service. I was
fortunate to know this in advance, so I was careful to negotiate hard on my
initial salary so that it was a rise on what I'd had previously and would cover
any rises I would forego for the next three years.

To match industry salaries, everyone in GDS has an inflated "grade". It's not the
only department in this situation (MHRA has a similar problem), but it does lead
to some oddities. If you enter the Civil Service on a high salary, you're 
effectively screwed for pay rises.

To give an example:

 - Your base salary is £60,000 which is the top of Cabinet Office Band A
 - You have a "Recruitment and Retainment Allowance" of £18,000
   - basically this is to match industry salaries for particular specialisms
 - Your total salary is £78,000

Civil Service Pay Rises are currently capped at "1% of the mid-point of the band"
which means that before tax, your pay rise is about £500/yr or 0.6% - which is 
a less than inflation, so in real terms your pay drops every year.

I'm entirely aware that this (completely fictional) example is a stonking salary
and people have to survive on a lot less, but still being worth less and less
each year does grate a bit.

## 4. The civil service stack-ranking performance management, keyed to generalists and widely discredited in Industry.

The civil service employs a box-ranking scheme where it expects you to be marked
against the Civil Service Competency Framework (which is entirely keyed to
generalists) and put into a box of basically doing great, doing OK and doing badly.

Pretty much every major organisation which did this (Yahoo, Microsoft) at any 
point had ditched the practise long before I joined the Civil Service. It's an
utterly crap and majorly demotivating way to manage people. It should die, in a
fire. It's being widely trashed (search for "Stack Ranking") and the Civil
Service should abandon it and stop trying to measure 400,000 people against the
same scale - it just doesn't work.

## 5. Conclusion

I hope this hasn't put you off joining the Civil Service. It's a great place to
work for a while. All the people are lovely. 

It's just the organisation that needs to change before I will go back. I'm sure 
it will and I'm sure I will, I just can't say when.
