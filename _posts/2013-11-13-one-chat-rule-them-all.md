---
layout: post
title: One Chat to Rule Them All
---
## Reducing the number of chat clients reduces distractions

If like me, you are a child of the internet generation, you've probably found that you have multiple
types of "chat" or social media on which people regularly interact with you. This article talks about
how you may be able to reduce this to manageable number, using ZNC and Bitlbee.

I recently reviewed my chat applications and found the following:

- Work Google Chat
- Personal Google Chat
- IRC
- 37Signals Campfire
- Facebook Chat
- Skype (both voice and group chatrooms)
- MSN
- ICQ
- Twitter

I previously used a variety of chat clients:

- Adium (for Google Chat, MSN, ICQ, Facebook)
- Twitter App
- Textual (for IRC)
- Skype
- Flint (for Campfire)

Having all of those chat clients open turned out to be a massive distraction,
as I was constantly cycling through the list to find the latest updates or
message on any one of the various configured IM networks.

This lead me to the idea of rationalising all of my chats into one client, to
reduce the number of places where I would be interacting with chat-type applications.

I first looked at Adium, which is an absolutely awesome chat client for OS X. It has
all of the major IM networks I use already configured and it's possible to make it
work with Campfire, IRC, Skype and Twitter. Conceivably that would reduce the number
of clients to 1, which would be absolutely awesome, but for the following issues:

- I really don't like Adium's interface for IRC-type chats - I'm much more comfortable
  with a more traditional IRC interface.
- Skype support is pretty rubbish (this is a problem with the non-open nature of Skype,
  any chat client needs to also keep Skype open which is a problem with Skype, not a
  problem with any open client).
- I'd have to sync my Adium config across 3 computers and I'm really lazy.

I decided what I'd actually prefer, was all my chats to look like IRC, rather than all
my IRC to look like chats — but is that really possible?

It turns out the answer is pretty much yes, for my use-case.

Given that you have a server on the internet, you can:

1. Setup ZNC which will be your connection point.
2. Use ZNC to proxy all of your regular IRC connections.
3. Setup Camper_Van to proxy from Campfire to ZNC
4. Setup Bitlbee to proxy IM and Twitter to IRC
5. Connect your favourite IRC client to ZNC
6. Profit!!!

For some uses (e.g. from home), I connect to ZNC from my existing Textual app (it's
actually 3 connections, one for Freenode IRC, one for CamperVan and one for Bitlbee,
but it's sufficiently simple that I can configure a new client from memory just by
setting up 3 IRC server connections).

On my work computer, where I'm stuck in a Terminal most of the time, I have taken
the time to setup Weechat on the same server as my ZNC bouncer, which enables me to
have a single SSH connection open to my server and then to use my existing weechat
profile to connect to all my regular IRC networks.

Hopefully the above has given you some ideas about how you can replace every chat
client with IRC. Even if you can't or won't do that, I would encourage you to simplify
your chat needs to as few different programs as possible — you will find the benefits
of fewer distractions worth it in the long run.
