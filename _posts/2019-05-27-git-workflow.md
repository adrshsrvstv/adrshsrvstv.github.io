---
layout: post
title: "A simple git workflow that works."
description: "git is hard and confusing. Here's some clarity."
date: 2019-05-27
tags: [git, code]
comments: true
share: true

---



# Basic git

Branches in Git are incredibly lightweight as well. They are simply pointers to a specific commit -- nothing more. a branch essentially says "I want to include the work of this commit and all parent commits."

## Rebase

`https://git-scm.com/docs/git-rebase`

Assume the following history exists and the current branch is "topic":

```
      A---B---C topic
     /
D---E---F---G master
```

From this point, the result of either of the following commands:

`git rebase master`
`git rebase master topic`
would be:

```
              A'--B'--C' topic
             /
D---E---F---G master
```

NOTE: The latter form is just a short-hand of git checkout topic followed by git rebase master. When rebase exits topic will remain the checked-out branch.

If the upstream branch already contains a change you have made (e.g., because you mailed a patch which was applied upstream), then that commit will be skipped. For example, running git rebase master on the following history (in which A' and A introduce the same set of changes, but have different committer information):

```
      A---B---C topic
     /
D---E---A'---F master
```

will result in:

```
               B'---C' topic
              /
D---E---A'---F master
```

Here is how you would transplant a topic branch based on one branch to another, to pretend that you forked the topic branch from the latter branch, using rebase --onto.

First let’s assume your topic is based on branch next. For example, a feature developed in topic depends on some functionality which is found in next.

```
o---o---o---o---o  master
     \
      o---o---o---o---o  next
                       \
                        o---o---o  topic
```

We want to make topic forked from branch master; for example, because the functionality on which topic depends was merged into the more stable master branch. We want our tree to look like this:

```
o---o---o---o---o  master
    |            \
    |             o'--o'--o'  topic
     \
      o---o---o---o---o  next
```

We can get this using the following command:

git rebase --onto master next topic
Another example of --onto option is to rebase part of a branch. If we have the following situation:

```
                        H---I---J topicB
                       /
              E---F---G  topicA
             /
A---B---C---D  master
```

then the command

git rebase --onto master topicA topicB
would result in:

```
             H'--I'--J'  topicB
            /
            | E---F---G  topicA
            |/
A---B---C---D  master
```

This is useful when topicB does not depend on topicA.

A range of commits could also be removed with rebase. If we have the following situation:

```
E---F---G---H---I---J  topicA

```

then the command

git rebase --onto topicA~5 topicA~3 topicA
would result in the removal of commits F and G:

```
E---H'---I'---J'  topicA

```

This is useful if F and G were flawed in some way, or should not be part of topicA. Note that the argument to --onto and the <upstream> parameter can be any valid commit-ish.

In case of conflict, git rebase will stop at the first problematic commit and leave conflict markers in the tree. You can use git diff to locate the markers (<<<<<<) and make edits to resolve the conflict. For each file you edit, you need to tell Git that the conflict has been resolved, typically this would be done with

`git add <filename>`
After resolving the conflict manually and updating the index with the desired resolution, you can continue the rebasing process with

`git rebase --continue`
Alternatively, you can undo the git rebase with

`git rebase --abort`

## Branch forcing

You're an expert on relative refs now, so let's actually use them for something.

One of the most common ways I use relative refs is to move branches around. You can directly reassign a branch to a commit with the -f option. So something like:

`git branch -f master HEAD~3`

moves (by force) the master branch to three parents behind HEAD.

## GIT RESET

git reset reverts changes by moving a branch reference backwards in time to an older commit. In this sense you can think of it as "rewriting history;" git reset will move a branch backwards as if the commit had never been made in the first place.

If you do git `reset --hard <SOME-COMMIT>` then Git will:

Make your current branch (typically master) back to point at `<SOME-COMMIT>`.
Then make the files in your working tree and the index ("staging area") the same as the versions committed in `<SOME-COMMIT>`.
HEAD points to your current branch (or current commit), so all that `git reset --hard HEAD` will do is to throw away any uncommitted changes you have.

## REVERT

for changes that are already pushed, use this. will create a new commit corresponding to old work.

`git revert HEAD~3`
Revert the changes specified by the fourth last commit in HEAD and create a new commit with the reverted changes.

`git revert -n master~5..master~2`
Revert the changes done by commits from the fifth last commit in master (included) to the third last commit in master (included), but do not create any commit with the reverted changes. The revert only modifies the working tree and the index.

## CHERRY-PICK

Git Cherry-pick
The first command in this series is called git cherry-pick. It takes on the following form:

`git cherry-pick <Commit1> <Commit2> <...>`
It's a very straightforward way of saying that you would like to copy a series of commits below your current location (HEAD). I personally love cherry-pick because there is very little magic involved and it's easy to understand.

`git cherry-pick master`
Apply the change introduced by the commit at the tip of the master branch and create a new commit with this change.

`git cherry-pick ..master`
`git cherry-pick ^HEAD master`
Apply the changes introduced by all commits that are ancestors of master but not of HEAD to produce new commits.

`git cherry-pick maint next ^master`
`git cherry-pick maint master..next`
Apply the changes introduced by all commits that are ancestors of maint or next, but not master or any of its ancestors. Note that the latter does not mean maint and everything between master and next; specifically, maint will not be used if it is included in master.

`git cherry-pick master~4 master~2`
Apply the changes introduced by the fifth and third last commits pointed to by master and create 2 new commits with these changes.

## Arguments

Great! Now that you know about remote tracking branches we can start to uncover some of the mystery behind how git push, fetch, and pull work. We're going to tackle one command at a time but the concepts between them are very similar.

First we'll look at git push. You learned in the remote tracking lesson that git figured out the remote and the branch to push to by looking at the properties of the currently checked out branch (the remote that it "tracks"). This is the behavior with no arguments specified, but git push can optionally take arguments in the form of:

`git push <remote> <place>`

What is a <place> parameter you say? We'll dive into the specifics soon, but first an example. Issuing the command:

`git push origin master`

translates to this in English:

Go to the branch named "master" in my repository, grab all the commits, and then go to the branch "master" on the remote named "origin". Place whatever commits are missing on that branch and then tell me when you're done.

By specifying master as the "place" argument, we told git where the commits will come from and where the commits will go. It's essentially the "place" or "location" to synchronize between the two repositories.

Keep in mind that since we told git everything it needs to know (by specifying both arguments), it totally ignores where we are checked out!

## --fixup and --autosquash

Ever had to make a super tiny change - a typo or a variable name change when cleaning up your work? I usually used to end up doing the whole committing + rebasing + repositioning the commit. Git has a shortcut for that:

```bash
git commit --fixup 3495206b #<--The commit you want to modify. This could be a relative ref too. :)
git rebase -i --autosquash HEAD~n # where n is the number of commits you want to go back. Could just be the SHA of the commit previous to 3495206b

```

And that's it. the `--autosquash` option will position the new commit in the right place. You just have to save and exit (`:wq`).

## stash

To demonstrate, you’ll go into your project and start working on a couple of files and possibly stage one of the changes. If you run `git status`, you can see your dirty state:

```bash
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#      modified:   index.html
#
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#
#      modified:   lib/simplegit.rb
#
```

Now you want to switch branches, but you don’t want to commit what you’ve been working on yet; so you’ll stash the changes. To push a new stash onto your stack, run `git stash`:

```bash
$ git stash
Saved working directory and index state \
  "WIP on master: 049d078 added the index file"
HEAD is now at 049d078 added the index file
(To restore them type "git stash apply")
```

Your working directory is clean:

```bash
$ git status
# On branch master
nothing to commit, working directory clean
```

At this point, you can easily switch branches and do work elsewhere; your changes are stored on your stack. To see which stashes you’ve stored, you can use `git stash list`:

```bash
$ git stash list
stash@{0}: WIP on master: 049d078 added the index file
stash@{1}: WIP on master: c264051 Revert "added file_size"
stash@{2}: WIP on master: 21d80a5 added number to log
```

In this case, two stashes were done previously, so you have access to three different stashed works. You can reapply the one you just stashed by using the command shown in the help output of the original stash command: `git stash apply`. If you want to apply one of the older stashes, you can specify it by naming it, like this: `git stash apply stash@{2}`. If you don’t specify a stash, Git assumes the most recent stash and tries to apply it:

```bash
$ git stash apply
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#
#      modified:   index.html
#      modified:   lib/simplegit.rb
#
```

## log

For short and sweet logs:

```bash
git log --pretty=oneline --abbrev-commit -n 5
```

For longer versions:

```bash
git log -n 5
```

