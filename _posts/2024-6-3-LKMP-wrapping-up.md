---
layout: post
title: "LKMP - Wrapping up"
date: 2024-6-3
---

The past 12 weeks have have been such a joyful ride into the linux
kernel.  I started my mentorship program on March 1, 2024 - which was
the spring.  I’ve learnt so much about things in the kernel and had
really great office hours where I got to sit in meets with wonderful
people and make great connections.  This post is about my journey in
these three months. <br />

### Weeks 1 - 4
My initial goal going into the program was to write a device driver - but
I understood very soon that I was pretty naive because I hadn’t know at
the time what devicetree had and its significance within the kernel and
the power it gives.  I also didn’t know how to test patches and how one
had to set up the right environment to test code and rightly compile for
the given architecture. <br />

My initial spell fix and docs fix patches were in this stage where I
decided that I had to learn these things and hence began reading driver
code for a couple of hardware modules that I knew about. <br />

After this, I read about dtschema and learnt how to convert txt bindings
to yaml ones so that they allowed validation against DTS files. <br />

Towards the end of this period, Shuah introduced my fellow mentees and me
to Julia Lawall and the device_node auto cleanup project where it was
desired to remove calls to `of_node_put()` and invoke it implicitly at the
end of scope of the corresponding pointer with `__free(device_node)` written
at the initialization. <br />

### Weeks 4 - 8
In this period, I mostly worked on dtschema patches and occasionally on
`of_node_put()` patches.  I learnt a lot about dtschema and how it
validates the devicetree code.  I also went through the driver code to
look at the various `of_*()` calls that were made to look at all the
properties that were used and their type to add or remove any properties
that were present in the txt binding and made no sense (and even sometimes
errored or warned by the binding check, once it was converted to yaml).
<br />

This also helped me in my of_node_put() work as it I got to understand
`device_node` better and how it was used in various places in the code so
that I didn’t unnecessarily do any `__free()` to auto clean it up anywhere.
<br />

I also had a great time in the LKMP’24 discord server where there was
continuous discussion on the `of_node_put()` work as it was something new
in the kernel and everyone including me was excited.  <br />

### Weeks 8 - 12
During these final few weeks I wanted to solely concentrate on `of_node_put()`
work as my dtschema patches were now merged into the spi tree (the subsystem
which I largely focused on).  <br />

I wrote three patches to do auto-cleanup in soc/ti/ that went through
critical review from Julia off-list and I’m really thankful for it as it
shaped the patches to take a more perfect form.  <br />

After I sent it to the list, the kernel test bot complained that it couldn’t
compile it, which led to an interesting discussion and Julia and I worked on
a report (which is stilla a draft) to describe the issue and give a possible
solution, since this hadn’t really happened in the kernel and was something
new.  The draft report can be read [here](https://docs.google.com/document/d/16_hTLTgEIwAURGw3PS4gOJxnKxComMQsPg_0XcuKlzo/edit?usp=sharing).  <br />

Jonathan suggested a really clear and nice solution that I prepared as a
v2 and which is currently under review off-list.  I also concurrently
started working on a driver for a module that I had used a couple of
semesters ago but which had no support in linux.  So currently I’m
learning more stuff to write a good driver and hopefully get it merged
into the mainline kernel. <br />

The past 12 weeks have been so much fun.  Being an Electronics and
Communication Engineering student, I’ve learnt so much about devicetrees
and drivers.  <br />

I have also attended the first ever kernel meetup that happened in
Hyderabad, India (from where I’m from).  It was fun to meet people who
were already working in the field and getting to know about how things
happened and what was currently happening.  <br />

I would like to thank Max Brown, Rob Herring, Krzysztof Kozlowski and
Jonathan Cameron and also other maintainers and reviewers who have been
very patient with my patches.  <br />

I would especially like to thank Julia Lawall for carefully reviewing
my patches and helping me on the report.  <br />

Of course, I can’t thank Shuah Khan and Javier Carrasco enough for their
support throughout the program.  I have really enjoyed the office hours
every week and have learnt so much in this program.  <br />

'til next time, <br />
Kousik
