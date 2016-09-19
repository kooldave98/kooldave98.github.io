---
layout: post
title:  "Don't repeat yourself"
date:   2014-12-20 19:55:37 +0100
categories: dry coding
---
[DRAFT: This is still a work in progress].
[Needs improvement: Needs better articulation]

When starting out as a software developer, the first thing that gets beaten into you is to never repeat yourself; that if you start to write the same thing over and over again, you should consider pulling it out into a common re-useable module.

While this is **very good advice**, I still have a few reservations about this based on my experience. First of- I never DRY my code until I have fully understood what its responsibilities are and have figured out what the strong boundaries/foundations(a framework that you think you can begin to build ontop ) are.

A lot of times, what seems to be similar code at the start ends up being very different things at a later stage.

You might say that I’m talking rubbish because you can always branch out when you realise your code starts to change, but this is where the problem actually lies.

The process of Software development can be likened to this: ![Yak shaving Gif here](/content/images/2015/08/yak-shaving.gif)

You go down into a context, and then again after a while into another sub-context, and so on and so forth… It becomes very easy to forget what the actual root goal was… and get lost deep down a hole.

When you eventually realise this, its too late, you’ve built up this huge infrastructure on an initial premise that has now turned out wrong. Time has been wasted, and you get depressed.
