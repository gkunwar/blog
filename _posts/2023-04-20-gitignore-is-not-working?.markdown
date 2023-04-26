---
layout: post
title:  ".gitignore is not working?"
date:   2023-04-20 18:59:44 +0545
categories: git
tags: git, github, gitlab
---

While working in a team, I always find complain about git from my team members(specially from new developer):

	"I just added a file to .gitignore but the changes from those files also appears when 
	I still see the changes with command: git diff”

I think this is not only my co-worker problem. Most new developers face this problem. So I thought to write a few notes on this topic.

The main problem is that most new developers forgot to clear the cache before committing changes related to .gitignore file.

So we need to clear cache and stage and commit the changes.

Here are simple steps which will solve this problem.

{% highlight git %}

git rm -r --cached .
git add .
git commit -m "fixed untracked files"

{% endhighlight %}
Hope it will help you if you are facing the same problem.