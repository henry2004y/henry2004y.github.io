---
layout: post
title: Version Control
tags: [computer]
comments: true
author: Hongyang Zhou
---

I haven't considered myself a programmer until very recent years. As a proof of that, 08/28/2017 is the first day I use Git.
Before mid 2019, our research groud were using CVS for version control. Back in 2005, Linus Torvalds, the creator of Linux, created Git in a very special scanerio: the Linux kernel community could no longer use their revision control system BitKeeper and no other Source Control Management (SCMs) met their needs for a distributed system.
Linus took the challenge into his own hands and disappeared over the weekend to emerge the following week with Git. In the same year, he made a [interval talk](https://www.youtube.com/watch?v=4XpnKHJAok8&t=2884s) at Google to explain his motivation.

Time proves Linus was right. Nowadays, Git the go-to option for revision control.
Quoted from his own word:
> I think that many others had been frustrated by all the same issues that made me hate SCM’s, and while there have been many projects that tried to fix one or two small corner cases that drove people wild, there really hadn’t been anything like git that really ended up taking on the big problems head on. Even when people don’t realize how important that “distributed” part was (and a lot of people were fighting it), once they figure out that it allows those easy and reliable backups, and allows people to make their own private test repositories without having to worry about the politics of having write access to some central repository, they’ll never go back.

I happen to know somebody who is strongly against Git but have to give up the fight and use it instead. So, what is wrong with CVS? By far the cleanest explanation I find is from Zack Brown:
> There were many complaints about CVS though. One was that it tracked changes on a per-file basis and didn't recognize a larger patch as a single revision, which made it hard to interpret the past contributions of other developers. There also were some hard-to-fix bugs, like race conditions when two conflicting patches were submitted at the same time.

CVS is really terrible when I want to reorganize the whole directory or the Internet connection is off.
Besides, I have some other opinions. The key concept behind Git is its distributed storage. I'll make a bet that if you are a truly open-source person, you will love this idea.

So now when you go back and revisit this story of Git, you can feel the importance of vision for the future. New things are born because we are tired of the old ones. The popularity of Git and its workflow has a reason.

By the way, for a serious project, NEVER push directly to the master branch. There are all kinds of tool to do automated testing before you are confident about the changes.

With all that being said, git is still not perfect. Recently I was confused about the usage of `git rebase`, so I did a Google search on the topic. Both of them are used for merging branches, but the differences are summarized [here](https://www.perforce.com/blog/vcs/git-rebase-vs-merge-which-better). Based on my current understanding, rebase is better than merge if you know what you are doing.

Here is a summary of [Git best practices](https://deepsource.io/blog/git-best-practices/). Never or less, happy coding!
