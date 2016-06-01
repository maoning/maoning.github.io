---
layout: post
title: Most Useful Git Operations
excerpt: "A personal git cheatsheet"
categories: Git Terminal
comments: true
---

I am nowhere near to be a git expert. After using ClearCase as the version control tool for over a year,
git to me is an entirely new beast. One irritation I had using git was that it is pretty challenging
to memorize all the commands beyond git add, commit, and push. I would usually them up again and again
on StackOverflow, write them down on a scrap of paper and forget about them. Therefore, I am
dedicating this post to sum up all the most used git operations for me.

#### Delete All the Untracked Files and Directories

```bash
git reset --hard HEAD
git clean -f -d
```

#### Undo git add --all

```bash
git reset
```

#### Deliver changes to a new side branch
```bash
git checkout -b <side branch name>
git add --all
git commit -m "<message>"
git push origin <side branch name>
```

#### Deliver a side branch to main branch
```bash
git checkout master
git pull origin master
git merge <side branch name>  // Testing: make sure everything works
git push origin master
```
