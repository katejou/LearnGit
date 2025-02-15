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

when I have two branch on local, I want to merge them into one.

main:        c1 c2
feature:     c3 c4

I am on main branch, and I run: git rebase main

main: c1 c2 c3 c4(feature)

I am not sure about if the feature branch is deleted ? <--

But it simply change the history of the fork, 
it make it seems like c3 and c4 were happened after c1 and c2.
And It look like I have never fork any branch to myself.

Don't do rebase after push the branch to remote because it might change other's history. And cause conflict.

## undo

undo

r2 r3
