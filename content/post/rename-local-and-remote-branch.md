+++
title = "Rename Local and Remote Branch"
description = "Fix your bad branch for great good"
date = 2019-02-26T11:03:01-06:00
draft = false
tags = ["git"]
comments = false
slug = ""
showpagemeta = false
showcomments = false
+++

We've all been there: cloning the project, making changes in our local branch, then commiting those changes to the repository, only to find you didn't follow the contribution guidelines for branch naming. Recently, I opened a merge request against the [docs for GitLab](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/25498), but didn't follow our documentation guidelines for [branch naming](https://docs.gitlab.com/ee/development/documentation/index.html#branch-naming) as I should have.

Initially, I created my branch: `add-efs-warning`, commited my changes and opened up the merge request. However, this was wrong as the branch name _also_ needs to be prefixed with `docs/`, `docs-`, or `-docs`. Rather than copying the changes I made to a blank text file, changing to the master branch, deleting the old branch, then creating a new branch and applying the changes, I learned how to rename my local branch _and_ remote branch.

Let's say you did the exact same thing I did and you're on your wrongly named local branch -- let's call it `bad-branch-name`. If you want to rename the branch, you can run:

```shell
git branch -m docs/new-branch-name
```

This will rename the current local branch to `docs/new-branch-name` and avoid feedback from the technical writers that review your changes. Next, you can run the following commnand to rename `bad-branch-name` to `docs/new-branch-name` and push the new local branch:

```shell
git push origin :bad-branch-name docs/new-branch-name
```

Finally, you can reset the upstream branch for the new local branch (switch to the branch if you're not currently working in it):

```shell
git push origin -u docs/new-branch-name
```

