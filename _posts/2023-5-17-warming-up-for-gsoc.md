---
layout: post
title: "Warming up for GSoC'23"
date: 2023-5-17
---

I have been accepted for GSoC'23 as a contributor! I will be contributing
to Git and the project I will be working on is

<br />
<strong> Unify ref-filter formats with other --pretty formats </strong>
<br />

My proposal can be read at [GSoC-Proposal](https://docs.google.com/document/d/1JBznA5n0WdWsbEskCeXxOnQuaa0urD89VtprxstLPzo/edit?usp=sharing).
<br />

The Git Community has been very supportive and I have learnt so much
in the time I spent with them before GSoC. Hoping that I will
continue to learn while working on this project and bond more
with the community.
<br />

My mentors are
<br/>
	Christian Couder &lt;christian.couder@gmail.com&gt; <br />
	Hariom Verma &lt;hariom18599@gmail.com&gt;
<br />

The main code repo, where I'll be working at is [repo](https://github.com/five-sh/git).
<br />

#### What Now?
I am currently working on the duplication of the logic, in pretty, in
ref-filter. Especially on the patches that Nsengiyumva Wilberforce sent
regarding the duplication of logic that formats commit and tag signatures.
Nsengiyumva's patches can be read on the [mailing list](https://lore.kernel.org/git/20230311210607.64927-1-nsengiyumvawilberforce@gmail.com/).
<br />

These patches seem to breaking CI, so I am working on them (see [branch](https://github.com/five-sh/git/commits/sign1))
as they are really helpful in accomplishing the goal of this project.
<br />

The code for the files `ref-filter.{c, h}` and `pretty.{c, h}` can be read
at the [git repo](https://github.com/git/git).
<br />

I will be updating this blog weekly on Wednesdays, tracking my progress
in that week.

'til next time, <br />
Kousik
