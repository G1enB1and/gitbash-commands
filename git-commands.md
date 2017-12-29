# git commands:  

## To start a new local empty repository:  
Before you can make commits or do anything else with a git repository, the  
repository needs to actually exist.  
To create a new repository with Git, we'll use the `git init` command.  

`git init` creates a new, empty repository in the current directory.  

The `init` subcommand is short for "initialize", which is helpful because it's  
the command that will do all of the initial setup of a repository.  

## To clone an existing git repository:  
`git clone` downloads a copy of an existing repository to the current working directory.  
Current working directory must not already be a git repository.  

Pass the url to an existing git repository by putting the url after `git clone`  
like this: `git clone https://github.com/udacity/course-git-blog-project`  

optionally, you can pass a new repository name after the url to clone an  
existing repository to a new name. Like this:  
`git clone https://github.com/udacity/course-git-blog-project new-repo-name`  

Don't forget to `cd` into the newly cloned directory before attempting any  
other git commands on it.  

## To start with an existing local directory and files:  
If you want to start version-controlling existing files (as opposed to an  
empty directory), you should probably begin tracking those files and do an  
initial commit. You can accomplish that with a few git add commands that  
specify the files you want to track, followed by a git commit:  

`git add *.c`
`git add LICENSE`
`git commit -m 'initial project version'`

We’ll go over what these commands do in just a minute. At this point, you have  
a Git repository with tracked files and an initial commit.  

# Other git commands:  
`git status` displays information such as which files are in which states.  

## git add  
`git add`  moves a file or files to the staging area. files in the staging area are monitored for changes, but not yet commited. `git add` can also be refered to as staging.  
`git add file1 file2 file3` or `git add .` the `.` means ALL files in the git init working directory.  

## git rm --cached  
`git rm --cached` removes a file or files from the staging area. This does not remove the files from the working directory or the repository, just the staging area.  

## git commit  
`git commit` requires a message to commit changes to the repository online.  
It will attempt to open your code editor first. If it cannot, then it will display  
`Aborting commit due to empty commit message.`  
If bash can open a code editor it will show a file named COMMIT_EDITMSG with information about what files will be committed and a comment instructing you to add a message to the file.  
Type a message on line 1, save the file, then close the editor (not just the tab). Then the bash terminal will update to show your commit message and files changed.  

you can bypass the editor and add the commit message in bash with:  
`git commit -m "message goes here"`  

## changing the last commit  
`git commit --amend`  
If your Working Directory is clean (meaning there aren't any uncommitted changes in the repository), then running `git commit --amend` will let you provide a new commit message for the last commit made.  
Your code editor will open up and display the original commit message. Just fix a misspelling or completely reword it! Then save it and close the editor to lock in the new commit message.  

## Add forgotten files to a commit  
Alternatively, `git commit --amend` will let you include files (or changes to files) you might've forgotten to include. Let's say you've updated the color of all navigation links across your entire website. You committed that change and thought you were done. But then you discovered that a special nav link buried deep on a page doesn't have the new color. You could just make a new commit that updates the color for that one link, but that would have two back-to-back commits that do practically the exact same thing (change link colors).  

Instead, you can amend the last commit (the one that updated the color of all of the other links) to include this forgotten one. To do get the forgotten link included, just:  

- edit the file(s)  
- save the file(s)  
- stage the file(s)  
- and run `git commit --amend`  

So you'd make changes to the necessary CSS and/or HTML files to get the forgotten link styled correctly, then you'd save all of the files that were modified, then you'd use git add to stage all of the modified files (just as if you were going to make a new commit!), but then you'd run `git commit --amend` to update the most-recent commit instead of creating a new one.  

## What is a Revert?  
When you tell Git to revert a specific commit, Git takes the changes that were made in commit and does the exact opposite of them. Let's break that down a bit. If a character is added in commit A, if Git reverts commit A, then Git will make a new commit where that character is deleted. It also works the other way where if a character/line is removed, then reverting that commit will add that content back!  

## the `git revert` command  
`git revert <SHA-of-commit-to-revert>` will make a new commit that undoes everything that was done in the commit referenced by SHA.  
(this will pop open your code editor to edit/accept the provided commit message unless you add `-m "commit message here"`)

## Reset vs Revert  
Reverting creates a new commit that reverts or undoes a previous commit. Resetting, on the other hand, erases commits!  

## Resetting is Dangerous!
You've got to be careful with Git's resetting capabilities. This is one of the few commands that lets you erase commits from the repository. If a commit is no longer in the repository, then its content is gone.  

To alleviate the stress a bit, Git does keep track of everything for about 30 days before it completely erases anything. To access this content, you'll need to use the `git reflog` command.  

## git reset command (dangerous)
`git reset <reference-to-commit>`  can be used to:  
- move the HEAD and current branch pointer to the referenced commit  
- erase commits  
- move committed changes to the staging index  
- unstage committed changes  

## git reset flags  
The way that Git determines if it erases, stages previously committed changes, or unstages previously committed changes is by the flag that's used. The flags are:  

- `--mixed` (default)  working directory gets or keeps changes removed from repository  
- `--soft`  staging index gets or keeps changes removed from repository  
- `--hard`  trash gets or keeps changes removed from repository  

`git reset --hard HEAD^` will take the changes made in the commit currently checkout out and pointed to by HEAD and erase them.  
  
## Relative Commit References  
You already know that you can reference commits by their SHA, by tags, branches, and the special `HEAD` pointer. Sometimes that's not enough, though. There will be times when you'll want to reference a commit relative to another commit. For example, there will be times where you'll want to tell Git about the commit that's one before the current commit...or two before the current commit. There are special characters called "Ancestry References" that we can use to tell Git about these relative references. Those characters are:  

- `^` indicates the parent commit  
- `~` indicates the first parent commit  

Here's how we can refer to previous commits:  

- the parent commit: the following indicate the parent commit of the current commit:  
    - `HEAD^`  
    - `HEAD~`  
    - `HEAD~1`  
- the grandparent commit: the following indicate the grandparent commit of the current commit:  
    - `HEAD^^`  
    - `HEAD~2`  
- the great-grandparent commit: the following indicate the great-grandparent commit of the current commit:  
    - `HEAD^^^`  
    - `HEAD~3`  

The main difference between the `^` and the `~` is when a commit is created from a merge. A merge commit has two parents. With a merge commit, the `^` reference is used to indicate the first parent of the commit while `^2` indicates the second parent. The first parent is the branch you were on when you ran `git merge` while the second parent is the branch that was merged in.  

## git diff  
The `git diff` command can be used to see changes that have been made but haven't been committed, yet.  The Output looks like `git log -p` because `git log -p` uses `git diff` under the hood. If there have not been any changes since last commit, nothing will happen.

## git log  

`git log` displays information about existing commits.  
Output uses `less` bash command to display one page at a time.
a colon `:` at the bottom left means there is more to display. You can navigate  
with `space` or arrows. Search with `/` or end with `q`.  

By default, this command displays:  
- the SHA
- the author
- the date
- and the message  
...of every commit in the repository. I stress the "By default" part of what  
Git displays because the git log command can display a lot more information  
than just this.  

You can specify a SHA (or just the first 7 digits of it) as the final argument to `git log` with any of the other options below to see only that one commits info. Like this: `git log -p fdf5493`  

`git log --oneline` will display just the first 7 digits of the SHA and the commits message on one line.  

`git log --stat` displays the files that have been changed in a commit and the number of lines that have been added or deleted.  

## git log --patch  

`git log -p` is a short form of `--patch`.  
It can be used to display the actual changes made to a file.  

the first line `diff --git a/file b/file` shows what file was changed. `a` is the original and `b` is the new. the `a` and `b` are not part of the path or name, they just indicate old and new. This is how you can tell if a file was renamed if `b/newname` is different from `a/oldname`.  

in the line `@@ -38,6 +38,11 @@`  
the `-` indicates the original file and `+` indicates the new changed file.  
`-38,6` indicates line number 38 and the following 6 lines of the original file. `+38,11` line 38 and the following 11 lines of the new changed file. 11, from 6 means that 5 lines were added in this area.  

## git log --decorate  
This flag has been enabled by default since git v2.13, so you no longer have to type it.
It shows tags to the right of commit SHAs.

## git log --graph  
adding `graph` to `git log` will add bullets and lines to the leftmost part of the output to indicate branching.

## git log --all  
adding `--all` to `git log` will show all branches in the repository.  

## git tag  
`git tag` will display all tags that are in the repository.  

`git tag -a v1.0` This will open your code editor and wait for you supply a message for the tag. How about the message "Ready for content"?  

CAREFUL: In the command above (`git tag -a v1.0`) the `-a` flag is used. This flag tells Git to create an annotated flag. If you don't provide the flag (i.e. `git tag v1.0`) then it'll create what's called a lightweight tag.  

Annotated tags are recommended because they include a lot of extra information such as:  

- the person who made the tag  
- the date the tag was made  
- a message for the tag  

Because of this, you should always use annotated tags.  

tags should be visible in logs by default since git v2.13, but if you don't see them, just type `git log --decorate`.  

### Adding a tag to a past commit  
By default, tags are applied to the most recent commit.  
If you want to specify a different commit, just append it's SHA number after the tag.
like this: `git tag -a v1.0 a87984`  

### deleting a tag  
`git tag -d v1.0` will delete the tag `v1.0`.  
`-d` is short for `--delete`  

### options for git log --patch:
`-w` ignores whitespace when comparing files.  

## git show  

`git show` displays information about the given commit by appending
it's SHA like this: `git show fdf5493`.

By default it shows:
- the commit
- the author
- the date
- the commit message
- the patch information  

However, `git show` can be combined with most of the same flags as for `git log`:  
- `--stat` to show the how many files were changed and the number of lines that were added/removed.
- `-p` or `--patch` this the default, but if `--stat` is used, the patch won't display, so pass `-p` to add it again.
- `-w` to ignore changes to whitespace.
