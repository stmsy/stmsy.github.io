---
title: Get Current Working Branch Name
tags:
  - GitHub
  - GitLab
  - Git
  - Shell
classes: wide
---

Due to the complicated naming covention, sometimes it is not easy to remember and type in your current working branch name. The following command let you get the branch name

```bash
git branch | sed -n -e "s/^\* \(.*\)/\1/p"
```

and you should be able to set the output to the variable

```bash
CURRENT_BRANCH=`git branch | sed -n -e "s/^\* \(.*\)/\1/p"`; git push origin $CURRENT_BRANCH
```

when you push your local branch to the remote.
