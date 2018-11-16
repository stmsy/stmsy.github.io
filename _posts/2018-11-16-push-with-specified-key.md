---
title: Push Local Branch with Specified Key
tags:
  - Git
  - GitHub
  - GitLab
classes: wide
---

If you register multiple SSH public keys on GitHub or GitLab, the following command will be helpful when pushing a local branch to the corresponding remote repo with the specified private key.

```bash
ssh-agent bash -c 'ssh-add path_to_private_key; git push -u origin branch_name'
```
