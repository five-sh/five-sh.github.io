---
layout: post
title: "The Final Report"
date: 2023-8-26
---

Hi, <br />
GSoC'23 is almost over and it is time for me to bring everything that I did in
the past 12 Weeks to a single place, including my work and the things that I
learnt and the relationship I have built with my mentors and the Git Community.

### Pre GSoC

My interest was piqued in Git back when I learnt what open source really was,
about a year ago. Since then I have been reading its code to get a feel of
it as it was something very different to the programming that I had been in
College or till that point of time. <br />

I still remember how I was lurking in the background of the mailing list every
day, seeing how things were done and was reading the code of Git's initial
commit, alongside, to see how they were translated into today's commands. <br />

These are the patches that I submitted to the mailing list before GSoC:
- [`[PATCH] repository-version.txt: partialClone casing change`](https://lore.kernel.org/git/20221110160556.29557-1-five231003@gmail.com/)
- [`[RFC][PATCH] object.c: use has_object() instead of repo_has_object_file()`](https://lore.kernel.org/git/20221116163956.1039137-1-five231003@gmail.com/)
- [`[PATCH] merge: use reverse_commit_list() for list reversal`](https://lore.kernel.org/git/20230202165137.118741-1-five231003@gmail.com/)
- [`[PATCH] commit: warn the usage of reverse_commit_list() helper`](https://lore.kernel.org/git/20230207150359.177641-1-five231003@gmail.com/)
- [`[PATCH v4] index-pack: remove fetch_if_missing=0`](https://lore.kernel.org/git/20230317175601.4250-1-five231003@gmail.com/)

A more detailed description about them can be read in my [GSoC Proposal](https://docs.google.com/document/d/1JBznA5n0WdWsbEskCeXxOnQuaa0urD89VtprxstLPzo/edit?usp=sharing).

### Project

__Title:__ Unify `ref-filter` formats with other `--pretty` formats <br />
__Mentors:__ Christian Couder, Hariom Verma <br />
__Aim:__ <br />
To unify both the `ref-filter` and `pretty` interfaces such that only a single
interface is used to handle the formatting of git's subcommands. <br />

As this is a continuation of the work done by other contributors, GSoC students
and Outreachy interns, my main goal in this project is to follow their path and
re-implement the remaining `pretty` placeholders into `ref-filter` formats.

### Work

Many of the `pretty` placeholders have already been implemented in `ref-filter`.
The ones that were remaining were the `signature` related formats, the
`describe` formats, the `mailmap` options and the `reflog` options. <br />

A more detailed mapping can be seen in this [transition table](https://docs.google.com/spreadsheets/d/1XKNbp1azKi2IFHzdkQSGS-dgnb98XM128lTXuszHTTA/edit?usp=sharing). <br />


#### The signature atom

The `signature` format and its friends give the commit and tag signature
information

``` sh
signature			- GPG signautre
signature:grade			- validity of the signature (good, bad, etc)
signature:signer		- signer of the GPG signature
signature:key			- key of the GPG signature
signature:fingerprint		- fingerprint fo the GPG signature
signature:primarykeyfingerprint - primary key fingerprint of the GPG signature
signature:trustlevel		- trust Level of the GPG Signature
```

The duplication of `signature` was something that was already worked on before
me. Almost all the work was done but one test was breaking CI, so I worked on
that and did some refactoring and sent the patches to the mailing list, which
have now been merged to master.


#### The describe atom

The `describe` atom and friends give the human readable form of a committish
by internally running `git-describe`.

``` sh
describe			- the raw output from git-describe on the given ref
describe:tags=<bool-value>	- along with annotated tags, consider light-weight tags as well if set
describe:abbrev=<number>	- use at least <number> digits to generate the human readable format
describe:match=<pattern>	- consider tags only that match the glob pattern
describe:exclude=<pattern>	- exclude all tags that match the glob pattern
```

These options can also be used together, where ever appropriate. <br />

The commits for this are also in master now. <br />


#### The mailmap options

The `mailmap` options are the usual name and email formats but respecting the
mailmap file at the top of a repository or according to relevant configuration
variable set.

``` sh
authorname:mailmap			- author name respecting mailmap
committername:mailmap			- committer name respecting mailmap
taggername:mailmap			- tagger name respecting mailmap

authoremail:mailmap			- author email respecting mailmap
authoremail:mailmap,trim		- author email without the angle brackets, respecting mailmap
authoremail:mailmap,localpart		- author email with only what occurs before '@', respecting mailmap
committeremail:mailmap			- committer email respecting mailmap
committeremail:mailmap,trim		- committer email without the angle brackets, respecting mailmap
committeremail:mailmap,localpart	- committer email with only what occurs before '@', respecting mailmap
taggeremail:mailmap			- tagger email respecting mailmap
taggeremail:mailmap,trim		- tagger email without the angle brackets, respecting mailmap
taggeremail:mailmap,localpart		- tagger email with only what occurs before '@', respecting mailmap
```

These formats are currently cooking in my fork and can be read on the branch
"[mailmap7](https://github.com/five-sh/git/commits/mailmap7)" which has the latest version of the commits associated with the
implementation of these formats. <br />

#### Misc

Apart from these, I also worked on using `ref-filter` logic wherever possible
in `pretty`. The way this is done is that if a mapping exists between
`ref-filter` formats and `pretty` formats, we use `ref-filter` logic. Otherwise,
we use the usual `pretty` logic. This is still cooking in my branch and is not
generally meant to be sent to the mailing list but can be used to check the
compatibility of any newly added formats. <br />

I also worked on a small patch which was a test fix in regards to how
`describe:abbrev=<number>` `pretty` format's test did not test all the possible
cases. This patch has been merged to master. <br />

I also made an attempt to review a patch that was sent to change a test that was
written as part of the original `signature` commits. While the review didn't go
as expected from my side (I misunderstood some meaning of the the patch), the
final patches looked very clean. This is the [mailing list thread](https://lore.kernel.org/git/20230821222448.1524a5fc@leda.eworm.net/T/). <br />

I have also maintained a [blog](https://five-sh.github.io/blog) during this period and have posted weekly about
the work I did in the week and also some other things. I hope to continue this
blog and post here whenever I find something to write about in Git that
fasicnated me or just anything tech-related in general.

### Patches


#### The signature atom

```
[Graduated to 'master']

* ks/ref-filter-signature (2023-06-06) 2 commits
  (merged to 'next' on 2023-07-06 at 1748d2bb93)
 + ref-filter: add new "signature" atom
 + t/lib-gpg: introduce new prereq GPG2
```

__Status__: Merged to master <br />
__Mailing List__: [Thread](https://lore.kernel.org/git/20230602023105.17979-3-five231003@gmail.com/T/) <br />
__Merge Commit__: [`ks/ref-filter-signature`](https://github.com/git/git/commit/81ebc54e81619ccc71fca6a4ce7822e78b24e80c)

#### The describe atom

```
[Graduated to 'master']

* ks/ref-filter-describe (2023-07-24) 2 commits
  (merged to 'next' on 2023-07-26 at f4b3b3b7ef)
 + ref-filter: add new "describe" atom
 + ref-filter: add multiple-option parsing functions
```

__Status__: Merged to master <br />
__Mailing List__: [Thread](https://lore.kernel.org/git/20230725205924.40585-3-five231003@gmail.com/T/) <br />
__Merge Commit__: [`ks/ref-filter-describe`](https://github.com/git/git/commit/70e5c5ddddadc7f15f64f812ae511eab83ca0040)

#### The mailmap options

```
ref-filter: add mailmap support
```

__Status__: Cooking in fork and passing tests <br />
__Fork__: [mailmap7](https://github.com/five-sh/git/commits/mailmap7)


#### Use ref-filter logic in pretty

```
pretty: use ref-filter logic wherever possible
pretty: introduce ref_format_commit()
ref-filter: introduce get_value_from_oid()
```

__Status__: Cooking in fork and failing tests <br />
__Reasons for failing tests__: <br />
- Around 10% of t4205, 30% of t4212 and 15% of t6006 seem to be failing tests.
- The `--date` option of `log` is not given higher priority when compared to the
  format string and this seems to be the main reason why the tests are failing.
- Some other tests are failing because of utf-8 formatting.
- The tests failures can be read in the [logs of ci](https://github.com/five-sh/git/actions/runs/5964643036) for this branch.

__Fork__: [use-ref-filter-in-pretty0](https://github.com/five-sh/git/commits/use-ref-filter-in-pretty0)


#### Test fix, describe with abbrev

```
[Graduated to 'master']

* ks/t4205-test-describe-with-abbrev-fix (2023-06-29) 1 commit
  (merged to 'next' on 2023-06-29 at 5fc309dc75)
 + t4205: correctly test %(describe:abbrev=...)
```

__Status__: Merged to master <br />
__Mailing List__: [Thread](https://lore.kernel.org/git/20230629133841.18784-2-five231003@gmail.com/T/) <br />
__Merge Commit__: [`ks/t4205-test-describe-with-abbrev-fix`](https://github.com/git/git/commit/d52a45cf5635f9f40a99ddc6efa92713f2d357b4)

### Future Work


#### The reflog formats

The `reflog` formats do not yet have an implementation in `ref-filter` and
an immediate thing to work on would be that. Of course, I'd like to come back to
it after sending the implementation of `mailmap` options to the mailing list and
making the work "use-ref-filter-in-pretty0" branch a bit more stable as it is
still failing tests. <br />


#### Refactor multiple option parsing functions

Another thing that one can work on is refactoring the multiple option parsing
functions that were introduced as part of the `describe` formats patches. <br />

There is a possibility that one could change the already existing functions in
`pretty` for multiple option parsing, which are `match_placeholder_arg_value()`
and `match_placeholder_bool_arg()`, so that they can directly be used in
`ref-filter` instead of `match_atom_arg_value()` and `match_atom_bool_arg().`

### Closing Remarks

This has been such a ride. I'm lucky to have such wonderful mentors,
Christian and Hariom, accept my proposal. They have guided me throughout this
project and have taught me so many things. They gave insightful reviews which
helped me improve my code quality and we often met through online meetings via
Google Meet, where they answered any questions that I had. I can't thank them
enough. <br />

I also want to thank the Git Community, which has been very supportive before
and during GSoC. From tolerating my sloppy patches to giving me very nice
explanations. Thanks Junio, Taylor, Peff, Elijah, Ævar, Jonathan, Oswald, Eric,
Glen and Calvin. <br />

I hope to continue in this community and keep learning things from them. <br />

'til next time, <br />
Kousik
