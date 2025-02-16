# Commands that I learn and pratice by myself 

## install git

xxx instal git

xxx = apt-get / yum / brew

depend on what pagkage management tools that you use at the time

## version

git version

type git (this will show where git have save its programs, response in : git is hashed xxx)

## make a git file
git init

git clone someurl

## config

cd to the .git file

ls and found the config file

## Level

system -- the uppest level, for it there are muti user in the compter

global -- the middle level, for personal user identity.（As a default setting to all local repo）

local -- the smallest level, for each repo only

In each level, each can set diffrent username and email.

SET:

git config --global user.name "name"
git config --global user.email "email@email.com"
git config --global init.defaultBranch main

CHECK:

git config --global --list

UNSET:

git config --global --unset user.name

## check status
git status

If you are in a middle of a failing merge / cherry-pic /etc and you need to abort it. You can find the solution here.

## modify
git add .

git add somefile

git add -p (only add some part of the file change)

git reset

## commit

git commit -m "Fix Something"

## Branching 1

we don't make change on the main branch usually.

CREATE (not switching to that)

git branch someBranchName

CHECK (how many banches and what branch we are on)

git branch -a

SWITCH (to the branch)

git checkout someBranchName

CREATE + SWITCH TO (the new branch at the sametime) 

git checkout -b someBranchName

## Viewing Local Changes

zone:

untracked -- outside of .git
tracked - Unmodified (commited)
        - Modified (unsaved)
        - Staged (saved)

### For viewing change in Modified:

git diff

### For viewing change in Staged:

git diff --staged

### For viewing change in Branch:

git diff someBranchName

- it compair the branch to the current branch I think...

## Merge

1. Switch to the branch that falls behind， that we want to merge changes into there.
2. CMD

git merge featureBranchName -m "someMessage"

3. merge is also a commit, so better type message.
4. there are merge strategies, 'ort' is the default one.
5. 'HEAD' is where the current newest step we are working in.


## Log

git log

(remember to quit by :q, hitting q)

git log --oneline

git log --oneline --graph

(we can see the merging realationship on the branch more easily by that, and we can delete unused branch after merge.)

## Branching 2

DELETE

git branch -d someBranchName

(after the delete, the branch names won't show on the log graph anymore)

## Put it on Severs/ Platform (remote)

So that we can work with others in the same project using Git.

1. Open a repo on that platfrom (Github)

2. Check my existing remotes (connection of the repo)

git remote      -> should show remote_name

git remote -v   -> show details includ url, both the push and fetch(/pull)

3. Add or Reset Remote

git remote add <remote_name> <new_url>

git remote set-url <remote_name> <new_url>

4. Make sure of the branch name

git branch -M main

5. Push

(remember to check if you have already add and commited all)

git push -u <remote_name> <branch_name>

git push -u origin main

-u: This is a shortcut for --set-upstream.  
It establishes a tracking connection between your local branch (in this case, main) and the remote branch (main on origin).  
This is important because it allows you to use simpler commands like 'git pull' and 'git push' in the future without having to specify the remote and branch every time.  

You only need to use -u the 'first time' you push a new branch to the remote.


e.g the remote only have a main branch, but we want to push a new feature branch to it.

git push -u origin feature

-> so the feature branch is built to the remote(which call origin)

and later we can use:

git push 

to do all the updates action.

## Branching 3

If you have pushed somehting on to the remote branch:

To delete a local branch that is already on remote sever，you have to delete the remote branch first.

1. Lists remote branches

git branch -r 

2. Or git push origin --delete feature_branch

git push origin -d feature_branch  

3. delete the local branch, after merging it to main branch

git branch -d feature_branch 

## Pull

1. From zero to one

git clone <http://....git>

2. update from others (saved on the remote)

git pull

pull = fetch + merge

3. What if I do fetch instead of pull

git fetch

git status (show my local branch is behind)

git diff main origin/main
(
    main = local main branch
    origin/main = remote main branch
)

git pull 
(to merge the remote branch after comfrim everything looks OK)


## Merge

Linear merge (main branch fall behind but stay the same, so it just catching up with the feature.)

3 way merge (main branch have a bit diffrent from feature, but they still can merge to together.
1. the split 
2. the main branch commit
3. the feature branch commit
so thats call the 3 way, in graph it looks like a Y fork have closed.
)

## Advance Merge -- Rebase

only use on local branching before pushing the branch to remote.
to keep a linear line, and make other easy to understand.

1. make a feature branch from main as usual, change a little and commit（f1）
2. make a little change to main branch, but not conflict to feature branch, than commit.(f2)
3. go to feature branch: git rebase main
4. the history of the feature branch will be changed, showing the (f2) happened before (f1) on this feature branch.
5. when go back to the main branch, nothing was affected, f1 still didn't exist in there.
6. on main brach: git merge feature
7. the merge will keep a straight line (and that's the whole point!)
8. you can delete the feature branch a push the main branch to remote 


when I have two branch on local, I want to merge them into one.

main:        f2
feature:     f1

I am on feature branch, and I run: git rebase main

main: f2 f1(feature)

It is not simply change the history f2, it clone a new f2, and delete the original one.
Their hash ID are not the same.  

Don't do rebase after push the branch to remote because it might change other's history. And cause conflict. （other's people computer have an other version of history）

--
I think this is useful the pull the new main branch before rebase/merge a feature branch. Your group memeber maybe fixed something while you are working on your own feature branch.
--

## Merge Conflict

1. when other change the main branch and push to remote
2. when you change the same thing on you local feature branch
3. you pull the main branch from remote to local main branch
4. you try to merge your feature brach to main branch
5. error message shown, to see more detail: git status
6. locate and open the file, depend on what editor you use, fix the conflict.
7. git add and commit this version, (, delete the feature branch?) then push.

## Reduce Conflict

1. Standardize Formatting Rules
2. Small and Frequent Commits(So that you version won't be too diffrent than others)
3. Communicate and Pay Attention

## Extra
1. to create a quick loop of commits
:for d in {1..6}; do touch "file${d}.md"; git add "file${d}.md"; git commit -m "adding file ${d}"; done

## Amend

git commit --amend

This cmd can fix the commit where the HEAD is pointing to
1. git log --oneline
(To check the Head pointer)

2. git commit --amend
(
It will Open a vim editor

Hit 'i'
i= insert mode (a --INSERT-- will show on the bottom)

By that, you change the first line, which is the commit message, or anything you can see in there.

Hit'esc' to jump out of the insert mode
Hit ':' to input instruction, type 'wq'.

:wq = save the writing and quit

)

3. git log --oneline

you can see the commit meassge is changed so as the hash ID

use pipe head to show only the last 10

$ git log --oneline | head


4. And this amend do not affect the remote at all! None of you teammates needs to know about it!

## Reset

1. git reset --soft 
(committed > saved)

$ git reset --soft HEAD~2 (the number is the step you take)
or
$ git reset --soft dcffa44 (the hash commit ID is found by git log --oneline)
(and it will reture to that step on commit, so it won't work if you type the last step.)

2. git reset --mixed
(committed > unsaved)

Because it is the default mode of reset, just type:
$ git reset HEAD~2 (the number is the step you take)

3. git reset --hard
(committed > deleted all changes)

Becareful!! Don't use that, I have been a victim right now!
It really just wipe out everything you have made before that point!

$ git reset --hard 11ff211

(when I try this, 11ff211 was the ID of 'adding file 1', and then it wipe out 'adding file2-7', and all the changes I have made to this notes in between)

$git reset --hard Head~1


## Reflog & Cherry-pick

Reflog track where Head has been on local, within 90 days.

$ git reflog

This can let us found the hash commit ID which we 'reset hard' on.
That ID could save what have been throw away.

$ git cherry-pick 723e41e

723e41e is an example

1. commit [4a05afd]
2. commit [723e41e]
3. git reset --hard 4a05afd
4. the second commit and all its changes is gone
5. git cherry-pick 723e41e
6. the second commit and all its changes is back
7. Yet the lastest commit ID is changed (check by log or reflog)

cherry-pick can recover commits that happen long ago.
but that commit must not conflict to all the files fight now.
which is very difficult and rare in use case.


# Popular Team Workflows

1. Basic
only one main branch, usually a solo project.

2. Feature Branch

Main > many feature branch

good for CICD
bad for having too many version and branches, too confusing

(release brach, deployment branch, production environment, testing environment...)

3. Git Flow
most common in larger teams

Main > Develop > many Feature branch

Develop branch is one more layer of testing and review, between feature and main.

In case features don't work well together.

With develop branch, the main branch can have a cleaner records of commits.

Bad for slow process of reviews.
May create for merge conflicts for more branches to begin with.
And therefore need more communitcation.

# Go to CourseResources.md for more