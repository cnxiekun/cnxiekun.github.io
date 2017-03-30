---
title: How to work with git
date: 2017-03-30 13:56:35
categories: Technique
tags: Git
description:
---

## Installing Git on Mac OS
On Mac OS X, a one-click installer package is available that can be downloaded from here: 
[link](https://code.google.com/p/git-osx-installer/downloads/list?can=3)

Once this is installed, you can jump right into Git by starting "Terminal.app" on your Mac.

## Configuring Git
A couple of very basic configurations should be made before you get started. For example, set your name and email address as follows:

```bash
$ git config --global user.name "John Doe"
$ git config --global user.email "john@doe.org"
```

<!--more-->

## Create a local repository
you can use the following commands to creat an empty local repository:

```bash
$ cd path/to/project/folder
$ git init
```
    
Now look at the files in that directory (including any hidden files):

```bash
$ ls -la
```
    
You'll see that a new, hidden folder was added, named ".git". 

## Clone a remote repository
you can get access to a remote repository on a server by using "git clone" command, for example:

```bash
$ cd your/development/folder/
$ git clone https://github.com/gittower/git-crash-course.git
```

On doing this, Git will now download a complete copy of this repository to your local disk - on condition that you're allowed to access this repository.

## Working on a project

### Staging area 
In Git, simply making some changes doesn't mean they're automatically committed to the local repository. The staging area allows you to determine which of your local changes shall be committed. 

You can stage some changes with the "git add" command:

```bash
$ git add new-page.html index.html css/*
```

With this command, we added the new "new-page.html" file, the modifications in "index.html", and all the changes in the "css" folder to the Staging Area.  

If you want to record the removal of some file in the next commit, you may use

```bash
$ git rm <filename>
```

You can also see what you've changed since your last commit using:

```bash
$ git status
```

### Committing changes    
Now you are ready to commit changes to local repository. The following command wraps up your changes:

```bash
$ git commit -m "First commit"
```
    
the commit message after "-m" is usually a short summary of your changes (up to 50 characters as a guideline). It will make it easier to understand what happened for you, as well as your teammates.
  
The following command is used to display the project's commit history:

    $ git log  

### Branching and Merging  
You are always working on a certain branch (the currently active, or "checked out", or "HEAD" branch). "git status"
will show you which branch is HEAD in its first line. The default is "master".

You can create a new branch using 

```bash
$ git branch newfeature
```

Now there exists two branches, namely "master" and "newfeature". You may switch to the new branch using:

```bash
$ git checkout newfeature
```

Running "git status", you'll see the HEAD is now "newfeature". Now you can work on this new branch, with
any other branches unaffected. 

You can merge the changes from the new branch into "master" using:

```bash
$ git checkout master
$ git merge newfeature
```
  
## Share work via remote repository 
Suppose you are connected to a remote repository "origin". You may integrate the remote changes into local repository using:

```bash
$ git fetch origin
```
    
or directly integrates them into your working copy using

```bash
$ git pull
```
    
It's actually a "fetch" command (which only downloads data) and a "merge" command (which integrates this data into your working copy) combined.

in case no tracking connection was established for your local HEAD branch, you will have to tell Git from which remote repository and which remote branch you want to pull ("git pull origin master", e.g.)

The following command uploads all the new commits from our current HEAD branch to its remote counterpart branch:

```bash
$ git push
```

That's it, enjoy it!