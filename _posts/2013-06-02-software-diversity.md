---
layout: post
title: Software Diversity on GOV.UK
---
After a talk by [Jordan](http://jordanh.net/) and [Tom](http://tom.loosemore.com/)
at the [OpenTech 2013 Conference](http://www.opentech.org.uk/2013/) conference recently,
I was asked if [the number of technologies we use](http://digital.cabinetoffice.gov.uk/govuk-launch-colophon/)
scares us. I thought this was an excellent question which leads to lots of interesting 
points about diversity which I would like to explore here.

GOV.UK is a diverse collection of individual applications and supporting services.
We operate at least five different programming languages, three separate database
types, two versions of an operating system and other variations too numerous to
count. When issues arise, the first problem is often to determine which of these
many things are related to the problem.

### If all you have is a hammer, everything looks like a nail

The reason we operate such a diverse ecosystem is that we are focused on solving
real problems. Our first task is to understand the problem or need we are solving
and then to choose the best tool for the job. If we restrict ourselves to moulding
the need to the tools we already have, then we risk not solving the initial problem
in the best way possible for the end-user. By restricting software diversity or
enforcing rigid organisational standards on a project, there is a possibility of
descending into a cargo cult, where we simply repeat the same patterns and mistakes
in everything we make.

GOV.UK is designed as a set of modular applications that each fulfil a defined set
of needs. The code which generates the [maternity pay
calculator](https://www.gov.uk/calculate-your-maternity-pay) is completely different
from the code to publish [information from government departments](https://www.gov.uk/government/).
By having these independent pieces, we both make sure that the application is suitable
for the job and also allow ourselves to scale by having different people or teams
work on something independently.

### The advantages and challenges of code diversity

#### Advantages

_"using the best tool for the job"_

Sometimes the best tool for a job is not the one you are currently using. My colleague
[Nick Stenning](https://twitter.com/nickstenning) recently prototyped a
[new router](https://github.com/nickstenning/router) to direct requests to the right
applications in [Go](http://golang.org/) - yes, it could have been done in Ruby or
Python or another language we use elsewhere (we've created [a router in Scala](https://github.com/alphagov/router)
before), but Go is designed for massive concurrency which is a feature our router needs;
the code also has fewer dependencies. Implementing something similar in one of those
other languages would require many more lines of code (compare the Scala and Go versions);
more lines of code is more chance of errors.

_"minimises the impact of issues in one tool causing a problem across the entire site"_

We have patched some of our applications several times in the last few months due to
vulnerabilities in the [Rails application framework](http://rubyonrails.org/). If
every component application on GOV.UK was written in Rails, we would need to upgrade
every single application each time a new vulnerability was discovered. It's true
that using lots of frameworks means more possible bugs, but each one of those bugs
would have a smaller risk to the site.

_"encourages a wide variety of contributions and skills"_

Often developers who are comfortable in more than one language are more creative,
choosing the right tool and code pattern for the job. There is a tendency if you know
only one language of fitting the job to the patterns you already use, which may not
be the best approach.

At GDS we concentrate on hiring good developers who display a wide variety of skills.
We do not have a bias for the people being masters of the tools we already use, as
a good developer who can already use more than one language should have no difficulty
grasping another. We may also learn something new from them and the team will become
stronger as a result.


#### Challenges and how to mitigate them

_"breadth of knowledge required to operate"_

GOV.UK embraces the [DevOps](https://www.gov.uk/service-manual/operations/devops)
model. The Developers of an application are actively involved in [supporting that
application in Production](https://github.com/alphagov/whitehall/pull/583). While
that means that the breadth of knowledge is still large, the depth of that knowledge
is held within the application team who provide additional support. As an Operator,
I need to understand roughly how it works, but for the detail I can defer to the
experts.

_"large number of pieces that can break"_

Yes, we have a lot of things that can break, but if they do, large parts of the
site and content available to the public (our raison d'être) will live on. By breaking
a very complex site down into a number of small components, we do increase complexity,
but we vastly reduce the impact of a breaking change and hence the overall risk remains
low.

_"unfamiliarity with tools leading to poor quality"_

If a team chooses to implement something in a new tool, which none of them are
familiar with, that might lead to poor quality code. At GDS, we like
[Pair Programming](http://en.wikipedia.org/wiki/Pair_programming) - two people
collaborating on something generally increases the quality and can allow those
with more familiarity to teach those new to a tool. Once that piece of work has
finished, the pair can split up and pair with two new people, meaning that the number
of developers who are familiar with the code doubles quickly.

We also use other quality practices, for example [code reviews](http://en.wikipedia.org/wiki/Code_review)
which ensure the output of the pair is understandable and maintainable by others,
and [Test Driven Development](http://en.wikipedia.org/wiki/Test-driven_development), to
confirm our code works and to build up a regression test suite over time.

### Standardisation is still important

Prior to launch we used two separate Search tools, [Apache Solr](http://lucene.apache.org/solr/)
and [ElasticSearch](http://www.elasticsearch.org/); each one does roughly the same job and the
effort to convert applications to use either of them is relatively low. For that reason we
standardised to reduce complexity - shortly after launch, all of our applications were
converted to use ElasticSearch.

Imposing loose standards can sometimes reduce the support burden. We use Ubuntu Linux, but the
version (10.04 LTS) we were using prior to launch does not easily allow running some more recent
software applications we needed. We made a decision to install a more recent version
of Ubuntu Linux (12.04 LTS) on some of our machines, rather than pick a completely different
distribution of Linux, so that tools and knowledge could be shared.

### So is it scary?

Yes, software diversity can be scary, but sometimes scary things make us better. If you like
software diversity, [maybe you should work for GDS!](http://digital.cabinetoffice.gov.uk/jobs/)
