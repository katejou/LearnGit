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

## modify git
git add .

git add somefile

git reset

## commit

git commit -m "Fix Something"

## branching

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

For viewing change in Modified:

git diff

For viewing change in Staged:

git diff --staged

