---
title: Contributors Summit
date: 2017-08-03
by:
- Sam Whited
tags:
- community
summary: Reporting from the Go Contributor Summit at GopherCon 2017.
---

## Introduction

The day before GopherCon, a group of Go team members and contributors gathered
in Denver to discuss and plan for the future of the Go project.
This was the first ever event of its kind, a major milestone for the Go project.
The event comprised a morning session revolving around focused discussions on a
theme, and an afternoon session made up of round table discussions in small
break-out groups.

### Compiler and runtime

The compiler and runtime session started out with a discussion about refactoring
`gc` and related tools into importable packages.
This would reduce overhead in the core tools and in IDEs which could embed the
compiler themselves to do quick syntax checking.
Code could also be compiled entirely in memory, which is useful in environments
that don't provide a filesystem, or to run tests continually while you develop
to get a live report of breakages.
More discussion about whether or not to pursue this line of work will most
likely be brought up on the mailing lists in the future.

There was also a great deal of discussion around bridging the gap between
optimized assembly code and Go.
Most crypto code in Go is written in assembly for performance reasons; this
makes it hard to debug, maintain, and read.
Furthermore, once you've ventured into writing assembly, you often can't call
back into Go, limiting code reuse.
A rewrite in Go would make maintenance easier.
Adding processor intrinsics and better support for 128-bit math would improve
Go's crypto performance.
It was proposed that the new `math/bits` package coming in 1.9 could be expanded
for this purpose.

Not being all that familiar with the development of the compiler and runtime,
this for me was one of the more interesting sessions of the day.
I learned a lot about the current state of the world, the problems, and where
people want to go from here.

### Dependency management

After a quick update from the [dep](https://github.com/golang/dep) team on the
status of the project, the dependency management session gravitated towards how
the Go world will work once dep (or something dep-like) becomes the primary
means of package management.
Work to make Go easier to get started with and make dep easier to use has
already started.
In Go 1.8, a default value for `GOPATH` was introduced, meaning users will only
have to add Go's bin directory to their `$PATH` before they can get started
with dep.

Another future usability improvement that dep might enable, is allowing Go to
work from any directory (not just a workspace in the GOPATH), so that people can
use the directory structures and workflows they're used to using with other
languages.
It may also be possible to make `go install` easier in the future by guiding
users through the process of adding the bin directory to their path, or even
automating the process.
There are many good options for making the Go tooling easier to use, and
discussion will likely continue on the mailing lists.

### The standard library

The discussions we had around the future of the Go language are mostly covered
in Russ Cox's blog post: [Toward Go 2](/blog//toward-go2), so
let's move on to the standard library session.

As a contributor to the standard library and subrepos, this session was
particularly interesting to me.
What goes in the standard library and subrepos, and how much it can change, is a
topic that isn't well defined.
It can be hard on the Go team to maintain a huge number of packages when they
may or may not have anyone with specific expertise in the subject matter.
To make critical fixes to packages in the standard library, one must wait 6
months for a new version of Go to ship (or a point release has to be shipped in
the case of security issues, which drains team resources).
Better dependency management may facilitate the migration of some packages out
of the standard library and into their own projects with their own release
schedules.

There was also some discussion about things that are difficult to achieve with
the interfaces in the standard library.
For instance, it would be nice if `io.Reader` accepted a context so that
blocking read operations could be canceled.

More [experience reports](/wiki/experiencereports) are
necessary before we can determine what will change in the standard library.

### Tooling and editors

A language server for editors to use was a hot topic in the tooling session,
with a number of people advocating for IDE and tool developers to adopt a common
"Go Language Server" to index and display information about code and packages.
Microsoft's [Language Server Protocol](https://www.github.com/Microsoft/language-server-protocol)
was suggested as a good starting point because of its wide support in editors
and IDEs.

Jaana Burcu Dogan also discussed her work on distributed tracing and how
information about runtime events could be made easier to acquire and attached to
traces.
Having a standard "counter" API to report statistics was proposed, but specific
experience reports from the community will be required before such an API can be
designed.

### The contributor experience

The final session of the day was on the contributor experience.
The first discussion was all about how the current Gerrit workflow could be made
easier for new contributors which has already resulted in improvements to the
documentation for several repos, and influenced the new contributors workshop a
few days later!

Making it easier to find tasks to work on, empowering users to perform gardening
tasks on the issue tracker, and making it easier to find reviewers were also
considered.
Hopefully we'll see improvements to these and many more areas of the
contribution process in the coming weeks and months!

### Breakout sessions

In the afternoon, participants broke out into smaller groups to have more
in-depth discussions about some of the topics from the morning session.
These discussions had more specific goals.
For example, one group worked on identifying the useful parts of an experience
report and a list of existing literature documenting Go user experiences,
resulting in the experience report
[wiki page](/wiki/experiencereports).

Another group considered the future of errors in Go.
Many Go users are initially confused by, or don't understand the fact that
`error` is an interface, and it can be difficult to attach more information to
errors without masking sentinel errors such as `io.EOF`.
The breakout session discussed specific ways it might be possible to fix some of
these issues in upcoming Go releases, but also ways error handling could be
improved in Go 2.

## Community

Outside of the technical discussions, the summit also provided an opportunity
for a group of people from all over the world who often talk and work together
to meet in person, in many cases for the first time.
There is no substitute for a little face-to-face time to build a sense of mutual
respect and comradeship, which is critical when a diverse group with different
backgrounds and ideas needs to come together to work in a single community.
During the breaks, Go team members dispersed themselves among the contributors
for discussions both about Go and a little general socialization, which really
helped to put faces to the names that review our code every day.

As Russ discussed in [Toward Go 2](/blog//toward-go2),
communicating effectively requires knowing your audience.
Having a broad sample of Go contributors in a room together helped us all to
understand the Go audience better and start many productive discussions about
the future of Go.
Going forward, we hope to do more frequent events like this to facilitate
discourse and a sense of community.

{{image "contributors-summit/IMG_20170712_145844.jpg"}}
{{image "contributors-summit/IMG_20170712_145854.jpg"}}
{{image "contributors-summit/IMG_20170712_145905.jpg"}}
{{image "contributors-summit/IMG_20170712_145911.jpg"}}
{{image "contributors-summit/IMG_20170712_145950.jpg"}}

Photos by Steve Francia
