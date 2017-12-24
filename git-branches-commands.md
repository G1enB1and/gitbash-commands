# Git Branch Commands and Information  

## Viewing Branches  
`git branch` will list out the branches in a repository.
In this list, it will put an `*` in front of the current working `HEAD` branch.  

## Creating Branches  
`git branch sidebar` will create a new branch called sidebar.  
branches can be created at any previous commit by appending a SHA. Like this:
`git branch alt-sidebar 42a69f` will create a branch called `alt-sidebar` at the commit matching 42a69f.  

## Deleting Branches  
`git branch -d sidebar` will delete the branch named `sidebar`.  

One thing to note is that you can't delete a branch that you're currently on. So to delete the `sidebar` branch, you'd have to switch to either the `master` branch or create and switch to a new branch.  

Git won't let you delete a branch if it has commits on it that aren't on any other branch (meaning the commits are unique to the branch that's about to be deleted).  
If you switched to the `master` branch and tried to delete the `sidebar` branch, Git also wouldn't let you do that because those new commits on the `sidebar` branch would be lost! To force deletion, you need to use a capital D flag (like this: `git branch -D sidebar`).  

## Switching Between Branches  
Creating a new branch does not automatically switch to that branch. For that, you need `git checkout`.  
`git checkout sidebar` switches to the sidebar branch.  

It's important to understand how this command works. Running this command will:  
- remove all files and directories from the Working Directory that Git is tracking  
- (files that Git tracks are stored in the repository, so nothing is lost)  
- go into the repository and pull out all of the files and directories of the commit that the branch points to  

So this will remove all of the files that are referenced by commits in the master branch. It will replace them with the files that are referenced by the commits in the sidebar branch. This is very important to understand, so go back and read these last two sentences.  

(This simply means that you are switching to a potentially very different version of the same project with multiple different files and code within files. You will no longer see the project as it is reflected in Master if you are in a branch called sidebar, if sidebar or master change.)  

The funny thing, though, is that both `sidebar` and `master` are pointing at the same commit, so it will look like nothing changes when you switch between them. But the command prompt will show "sidebar", now:  

`git log` will show `HEAD->sidebar, master`  
`HEAD` is the current working branch, and it is pointing `->` `sidebar` as the current branch, then showing `master` as another branch in the repository.  
