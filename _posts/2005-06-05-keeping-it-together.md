---
layout: post
title: Keeping It Together
---
Adam has some interesting things to say about keeping config files in synch
across multiple hosts. The solution he presents of using a version control
repository to keep configs files which can be checked in and checked out across
hosts is an interesting one.

I do a lot of work with RedHat Network as we use it to manage our machines. It
has a concept of channels to which you subscribe which supply software
packages. There are also config channels that you can subscribe to which will
pull down sets of config files for you. This is great if you need to setup a
large number of identical machines - we don’t.

For user config files, there is another option - make your entire home
directory identical across a number of machines. In the Windows World (at
Imperial College at least) you get a Roaming Profile and a Network Home
Directory whenever you logon with a domain account. In the Unix world the same
thing has been true since the dawn of time, but more and more people are
forgetting this.

NFS was the traditional method for network storage - you have a network
fileserver with home directories for all your users and you mount this on all
the client machines - this is the method I use for my personal home directory.
It has however, a number of drawbacks:

1. anyone to whom you export the directories can read files if they are root on
   their own machine.
2. its only really designed for a single fileserver, there’s no real redundancy
   or scaleability

To get around one of these limitations, NFSv4
has been developed. This system is Kerberos aware and hence you can only read
and write files for which you have a relevant kerberos ticket. This fits in
well with our infrastructure, which is based on Windows Active Directory
servers as Kerberos servers. However it does raise a problem, in that it seems
each machine (both server and client) needs a service ticket for NFS within the
kerberos database. That would be easy if this was a genuine kerberos server,
but I have no idea (and I don’t think my windows brethren know either) how to
add a service ticket to the KDB in any automated fashion.

I’m still working on NFSv4, b ut it looks like it might involve something
complex like a seperate kerberos realm for NFS, with a cross domain (one way)
trust to the Windows KDC realm.

Something which gets around both of the original limitations is OpenAFS. An AFS
cell can exist across multiple fileserving machines, with each one keeping
track of changes to the underlying filesystem. And AFS is natively kerberos
aware… if only the tickets given out by a Windows KDC were AFS capable. Once we
sort out the ticketing issue, this one might be good to go.

So maybe at some point I’ll upgrade my fileserver to NFSv4 or AFS, but it may
take a while…
