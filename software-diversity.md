## Diversity is a good thing

At the [OpenTech 2013](http://www.opentech.org.uk/2013/) conference recently, after
a talk by my colleagues [Jordan Hatch](http://jordanh.net/) and [Tom 
Loosemore](http://tom.loosemore.com/), someone asked a question "I've read 
[the GOV.UK colophon](http://digital.cabinetoffice.gov.uk/govuk-launch-colophon/)
and seen the number of technologies you used, don't you find that scary?" which
is an excellent question and leads to lots of interesting points about diversity.

I am not a developer, I don't write the code behind the applications that form
part of GOV.UK, but as a member of the Infrastructure team, I do have a lot of
input into the day-to-day running of the website and Tom and Jordan were kind
enough to let me answer the question at the time, which now forms the basis of
this blog post.

GOV.UK is a diverse collection of individual applications and supporting services.
We operate at least five different programming languages, three separate database
types, two versions of an operating system and other variations too numerous to
count. When issues arise, the first problem is often to determine which of these
many things are related to the problem.

### If all you have is a hammer, everything looks like a nail

The reason we operate such a diverse ecosystem, is that we are focused on solving
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
from the code to publish [information from government departments](https://www.gov.uk/government/). By having these independent pieces, we both make sure that the 
application is suitable for the job and also allow ourselves to scale by having
different people or teams work on something independently.

### The advantages and challenges of code diversity

#### Advantages

- using the best tool for the job

Sometimes the best tool for a job is not the one you are currently using. My colleague
[Nick Stenning](https://twitter.com/nickstenning) recently prototyped a [new router](https://github.com/nickstenning/router) to direct requests to the right applications in
[Go](http://golang.org/) - yes, it could have been done in Ruby or Python or another
language we use elsewhere (we've done it in Scala before), but Go is designed for
massive concurrency which is a feature our router needs. Implementing something similar
in one of those other languages would require many more lines of code; more lines
of code is more chance of errors.

- minimise the impact of issues in one tool causing a problem across the entire site

If you look at the Rails framework recently you will see a number of critical security
vulnerabilities. If every component application on GOV.UK was written in Rails, we
would need to upgrade every single application each time a new vulnerability was
discovered. It's true that using lots of frameworks means more possible bugs, but
each one of those bugs would have a smaller risk to the site.

- encourage a wide variety of contributions

Not everyone is a Ruby developer. We have many excellent developers in GDS, many
of whom do not write Ruby as their first language. If we only made applications in
Ruby, we'd only need to recruit people who know Ruby, but we would be missing out
on a huge range of programming talent. Each one of our products recruits the best
people we can find and then uses the tools which they are familiar with to solve
the needs that have been identified. We've got some smashing Perl, some Scala, some
Ruby and some Python. As a Python guy, I'm OK with this.

#### Challenges and how to mitigate them

- breadth of knowledge required to operate

GOV.UK embraces the [DevOps](https://www.gov.uk/service-manual/operations/devops)
model. The Developers of an application are actively involved in supporting that
application in Production. While that means that the breadth of knowledge is still
large, the depth of that knowledge is held within the application team who provide
additional support. As an Operator, I need to understand roughly how it works, but
for the detail I can defer to the experts.

- large number of pieces that can break

Yes, we have a lot of things that can break, but if they do, large parts of the
site and content available to the public (our raison d'être) will live on. By breaking
a very complex site down into a number of small components, we do increase complexity,
but we vastly reduce the impact of a breaking change and hence the overall risk remains
low.

- unfamiliarity with tools leading to poor quality

If a team chooses to implement something in a new tool, which none of them are
familiar with, that might lead to poor quality code - some of that can be mitigated
by preferring tools with which we have at least some familiarity. At GDS, we like
[Pair Programming](http://en.wikipedia.org/wiki/Pair_programming) and [code reviews](http://en.wikipedia.org/wiki/Code_review) - two people collaborating on something generally
increases the quality and code review ensures that the output of the pair is
understandable and maintainable by others.

### Standardisation is still important

This is not to say that software standards have no place. Where it is sensible to
standardise we should, because that reduces complexity. For example, GOV.UK may be
composed of two operating system versions (Ubuntu Linux versions 10.04 and 12.04),
but they are broadly similar and hence knowledge can be transferred. That's
completely different to having a platform composed of two disparate operating
systems.

We also seek to standardise where it makes sense to do so. Prior to launch we supported
two separate Search technologies, [Apache Solr](http://lucene.apache.org/solr/) and
[ElasticSearch](http://www.elasticsearch.org/), each one doing roughly the same job. It
made sense to standardise on one technology if you are using multiple equivalent ones
and hence very shortly after launch, all of our applications were converted to using
ElasticSearch.

### So is it scary?

Yes, diversity can be scary, but sometimes scary things make us better. If you like
diversity, [maybe you should work for GDS!](http://digital.cabinetoffice.gov.uk/jobs/)
