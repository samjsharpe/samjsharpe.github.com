---
layout: post
title: Migrating GOV.UK to new infrastructure
---
On Tuesday night, we moved GOV.UK from one set of servers to another - with any luck, nobody noticed.

Much of what we do at GDS is designed to be noticed in some way, usually because we are trying to
change something for the better. However my definition of 'success' for a migration of a reasonably
complex website involving 160+ virtual machines from one place to another is that the public could
continue to use GOV.UK during the migration and the disruption to content creators within government
was minimised - in effect, nobody would notice.

We migrated:

- 100,000 items of content (webpages)
- 250GB of attachments (downloads from webpages)
- 20+ databases (ranging from 6MB to 6GB in size)
- The noticeable effects were:
  - **for ordinary users:** Applying for a Licence was disabled for 2.5 hours (between 6.00pm and 8.30pm)
  - **for government users:** Content could not be published for 90 minutes (between 6.00pm and 7.30pm)
    without manual intervention by the migration team (available by phone in emergencies)

That's not to say there weren't some minor issues (which will be covered in more detail below), but
the vast majority of GOV.UK was functioning to the general public for the entire duration of the
migration.

## Planning and Communicating the Move

My first rule of planning is:

> No battle plan survives contact with the enemy _- Helmuth von Moltke_

Given that it would take a disproportional amount of work to create a comprehensive plan that would cover
every possible eventuality of a fast moving environment like ours, we decided to:

- do enough planning to describe what should be done, to provide a checklist when actually doing the migration
- do enough planning to assess the likely risks, so that we can mitigate as many as possible
- defer some decision-making to the staff involved during the migration, where it makes sense to do so

Rather than re-describe the plan in detail, we've simply [published it](https://github.com/alphagov/govuk_migration_plan_public),
however we've replaced a small number of fine details such as IP addresses and domain names with examples.
The broad steps taken on the evening of migration are covered in the sections below, so you don't need to read
the entire plan to follow along.

## Preparation of Environments

Our migration strategy was to create a replica of our Production and Staging environments and copy the
important data across, discarding the old environments at a later stage. Provisioning  on VMware vCloud
has improved massively since we launched GOV.UK in October 2012 and that includes some work our
colleagues have done to create tooling which we were able to take advantage of to create the virtual
machines we needed.

The GOV.UK Infrastructure Team was in heavy demand during the earlier part of the year, so in order to
do this work (and take advantage of their experience), we contracted with Cloudreach (an SME specialising
in Cloud Infrastructure) via G-Cloud, to help us with creating the initial copy of our production
virtual machines. We then built a replica of our staging virtual machines using the documentation and
lessons learnt by Cloudreach.

Once we had created the virtual machines, we altered our deployment process so that each time an
application was deployed to the live servers, the same code would be deployed to the new servers. We also
created automated jobs which could copy data from old to new and ran them nightly. This ensured that the
code and data deployed on the new platform was equivalent to the existing systems.

In order to test that the new platform was working correctly, we ran our existing smoke tests continuously
against the new environment and worked through any errors until they passed. We also used Gor (as described
by my colleague Dan Carley in Putting the Router through its paces) to copy live traffic to the new platform
and ensure that no additional errors were seen.

This preparation meant that when we actually performed the migration, we were doing so to a comprehensively
tested platform and we were copying data with scripts we were already using regularly, minimising the
potential for errors.

## Moving the site (and some issues we experienced)

The move was planned for 6.00pm on a Tuesday. The reason being that historically, publishing activity is
quite low at that time. This would also allow time for a full migration AND a full rollback by 9.00am the
next day and mean that we didn't plan to have any of our limited staff working overnight.

Our migration involved:

- Blocking traffic to writeable parts of the site
- Syncing the data using our nightly sync scripts
- Switching services to the new infrastructure (via DNS)
- Testing the sites manually and with automated tests
- Opened the site up for publishing

## What went wrong

At one point, a couple of minutes after we transferred live traffic, the traffic completely stopped between
our Content Delivery Network (CDN) and the new virtual machines. It was due to a slight health check
configuration issue, which meant that our CDN had marked our working machines as having failed. Having
staff available who knew how that interaction worked, plus having early warning of the traffic flow, really
helped us to recover from this within a few minutes.

During the migration, we watched the live traffic to our servers with Logstalgia running on a large display.
This was configured at late-notice so we'd have something impressive to watch, as it provides a pretty 3D
visualisation of web traffic. However, it proved to be an excellent early warning mechanism as we could see
the traffic moving and more importantly we could see immediately when it stopped.

We also discovered about an hour after the migration was completed that we'd missed our Transactions Explorer
sub-site and it hadn't been copied to the new machines. Luckily this was responsible for only a very small
number of requests at that time of day and we were able to correct the error quickly. We've also added this
to our smoke tests to make sure it cannot happen again, but it proves that even very comprehensive testing
and planning can miss small details.

However, the fact this application was missed was quickly spotted by a committed developer taking it upon
themselves to check applications their team were responsible for, showing that if you have a team of engaged
and interested developers, you can trust them to do the right thing without prompting.

## Benefits of Migration

After all that work over many months, the natural question on anyone's mind would be "Why would you make
yourself do that?"

### Better platform

When we first launched GOV.UK, the market for Infrastructure as a Service (IaaS) that had been accredited
to handle some of our data was quite small. We were actually one of the first customers of Skyscape Cloud
Services and hence we were an early adopter of their first IaaS platform.

Since that time Skyscape have created a new, improved platform which benefits from the inevitable performance
increases of new technologies and were encouraging customers to move to this, so that they could focus their
resources on further improvements to one platform, rather than maintaining a legacy platform for these early
adopters.

### Improved Infrastructure

As we were already planning a move, it made a lot of sense to make some small improvements to our
infrastructure, especially where they would have been disruptive to make while running live services.

We now have:

- a consistent, supported Operating System (Ubuntu 12.04 LTS) rather than a mixture of 10.04 LTS and 12.04 LTS
- upgraded databases (MongoDB 2.4.9, MySQL 5.5) - upgrading a live database would have required a similar
  publishing outage
- applications split between different database clusters, so that the heaviest usage is spread across
  multiple machines
- consistent machine naming and sizing

### To prove we can

One of the principles of G-Cloud is to avoid signing up to multi-year contracts, so that we can take
advantage of improvements both in technology and price. The typical length of an IaaS contract on G-Cloud
is one year, with an option to extend.

However, there's no point having a one year contract if you don't have the ability at the end of it to
switch to something else. By proving that we could execute a move of our infrastucture within Skyscape,
we've also given ourselves more confidence that should we need to in future, we can move (or recreate
from scratch) GOV.UK within Skyscape or to a range of other IaaS providers.

## What we would change next time

Aside from the obvious points of "don't let the traffic stop and don't forget to copy transactions-explorer",
we'd like to improve this process each time we do it. The natural targets would be to reduce the downtime
for Apply for a Licence and Publishing, to reduce the impact on the end-users.

The limiting step on each of these is the time taken to copy the various MongoDB and MySQL databases - when
we sync the databases we copy the entire database from one machine to another, whereas for file copies we
use rsync to copy over only the changed files each time.

In the future we will be investigating either continuous replication of databases to a secondary location
which can then be promoted to being the live environment, or synchronising only the changes in the databases
(e.g. by replaying the transaction logs) - this could potentially be faster, but is more complex to execute
well.

----

This post was originally published on the [GDS Technology Blog](https://gdstechnology.blog.gov.uk/2014/03/28/migrating-govuk-infrastructure/)
