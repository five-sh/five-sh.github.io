---
layout: post
title: "GSoC'23 it's a wrap"
date: 2023-8-26
---

It's the last week of GSoC'23. What a beautiful ride it has been. I have learnt
so much in these past 12 weeks. <br />

In this last week, I wanted to wrap up my work on using `ref-filter` logic in
`pretty` wherever possible and I think it took a bit too long. <br />

The way this is done is the same as I wrote it out in the last post. The commits
are on the branch "[use-ref-filter-in-pretty0](https://github.com/five-sh/git/commits/use-ref-filter-in-pretty0)". They seem to be failing some
tests because some options, for example for `log`, don't really work like
they are expected to and since whenever we encounter a known `ref-filter`
format, we jump into `ref-filter` logic, some options are being over-ridden
because of this, although it should be mentioned that the grabbing of the values
for the formats is done by successively switching between `ref-fitler` and
`pretty`. So I think the functions need to be called more carefully, in
such a way that we fall back to `pretty`'s way of doing things.

I also made an attempt to review a patch that concentrated on a test regarding
the `signature` atom. Although it seems that I misunderstood the patch a bit and
the author was kind enough to explain to me in more detail what the patch was
really aimed at and after a bit of discussion, the author sent out two patches
as another way of doing this which was really clean. The discussion can be read
at this [thread](https://lore.kernel.org/git/20230821222448.1524a5fc@leda.eworm.net/T/).

I have summed up all my work and brought it together in [the final report](https://five-sh.github.io/2023/08/26/the-final-report). <br />

Thanks Christian and Hariom for mentoring me and teaching me a lot of things in
these past weeks. I have learnt so much and believe that my code taste has
improved a lot compared to when I took my first steps towards contributing to
Git. <br />

I have decided that I will continue to contribute to Git even after GSoC and
there are things in the code which I would like to work on. <br />

'til next time, <br />
Kousik
