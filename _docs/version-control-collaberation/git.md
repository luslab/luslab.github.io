---
title: Git
category: 4 - Version Control
order: 1
---

# What is Git?

placeholder

# git submodules

Submodules allow you to include or embed one or more repositories as a sub-folder inside another repository.

You can find more detailed explanation on sub-modules here:

1. [Git documentation](https://git-scm.com/book/en/v2/Git-Tools-Submodules)
2. [Github documentation](https://github.blog/2016-02-01-working-with-submodules/)

To add a submodule to a project start in the root of the target repository. To add a submodule from github:

`git submodule add https://github.com/<user/org>/target-repo target-local-folder`

This operation should add a `.gitmodules` file in the repo root. The file should look like this:

```
[submodule "luslab-nf-modules"]
    path = luslab-nf-modules
    url = https://github.com/luslab/luslab-nf-modules.git
```

The folder added to the project is essentially a static copy of the source repo. Git knows not to look through all the folder and try to commit all the changes. There will be a commit to be made of just the folder name which is expected.

To make the submodule updatable, add a branch indicator to the submodules file. You can set this `master` or any other branch you want from the source repo. Your `.submodules` file should now look like this:

```
[submodule "luslab-nf-modules"]
    path = luslab-nf-modules
    url = https://github.com/luslab/luslab-nf-modules.git
    branch = master
```

If there are changes in the source repo you wish to pull into your module, run the following command:

`git submodule update --remote`

After pulling down the changes create a new commit based on the changed folder hash in your local repo.