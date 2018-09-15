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

## create and switch to a branch in one line:
`git checkout -b new-branch-name` will create a branch called `new-branch-name` and switch to it.  
You can also append a SHA or branch name to that to start there.  

## undo a merge  
If you make a merge on the wrong branch, use this command to undo the merge:  
`git reset --hard HEAD^`  
(Make sure to include the `^` character! It's a known as a "Relative Commit Reference" and indicates "the parent commit".  

## merge  
`git merge <name-of-branch-to-merge-in>`  

The current checked in branch with the HEAD pointing to it is going to be the branch that moves ahead with the commit that merging makes and take in the other branch provided by name.  

When a merge happens, Git will:  
- look at the branches that it's going to merge  
- look back along the branch's history to find a single commit that both branches have in their commit history  
- combine the lines of code that were changed on the separate branches together  
- make a commit to record the merge  

When we merge, we're merging some other branch into the current (checked-out) branch. We're not merging two branches into a new branch. We're not merging the current branch into the other branch.  

## fast-forward merge  
A Fast-forward merge will just move the currently checked out branch forward until it points to the same commit that the other branch is pointing to.  

The command and syntax are the same, it just means the  branch being merged in is ahead of the checkout out branch, so it moves the checkout out branch ahead to catch up.  

After the merge, both branches will point to the same commit.  No new commit is made in a fast-forward merge.  

## merge conflicts  
If a merge conflict does occur, Git will try to combine as much as it can, but then it will leave special markers (e.g. `>>>` and `<<<`) that tell you where you need to manually fix.  

## what causes a merge conflict  
As you've learned, Git tracks lines in files. A merge conflict will happen when - the exact same line(s) are changed in separate branches -. For example, if you're on a alternate-sidebar-style branch and change the sidebar's heading to "About Me" but then on a different branch and change the sidebar's heading to "Information About Me", which heading should Git choose? You've changed the heading on both branches, so there's no way Git will know which one you actually want to keep. And it sure isn't going to just randomly pick for you!  

Changes made ahead of the checked in branch will not cause merge conflicts even when the same line is changed on both branches because this is a fast-forward type of merge in which the newer change takes priority and replaces older changes with no conflict.  

## merge conflict indicators in the code editor
The code editor will add the following to your code to indicate merge conflicts:  

- `<<<<<<< HEAD` everything below this line (until the next indicator) shows you what's on the current branch  
- `||||||| merged common ancestors` everything below this line (until the next indicator) shows you what the original lines were  
- `=======` is the end of the original lines, everything that follows (until the next indicator) is what's on the branch that's being merged in  
- `>>>>>>> heading-update` is the ending indicator of what's on the branch that's being merged in (in this case, the `heading-update` branch)  

## resolving a merge conflict  
To resolve the conflict, you must delete the lines added to the code editor indicating merge conflicts and either pick one line to keep, or delete both and make a new one, then save, add, and commit.  

Be careful that a file might have merge conflicts in multiple parts of the file, so make sure you check the entire file for merge conflict indicators - a quick search for <<< should help you locate all of them.

It is common practice to leave this message blank, let it open the code editor to supply a message and just close it to confirm the default message.  

If you forget to remove lines that were added to indicate merge conflict information, those will be committed as part of your code!  
