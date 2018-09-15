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
<<<<<<< HEAD
`git commit` opens the code editor associated with bash, shows you what branch your on and the files being commited and prompts you to add a message to the commit.  
  
||||||| merged common ancestors
`git commit`  

=======
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

>>>>>>> 703924daedbacd491a69fc58d5e4ab58ae5b89c8
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

# Remote Repositories  
Up until now everything (even commits) have been local. Following are some commands and information to work with remote repositories like GitHub. Branches can be merged and pushed to the remote at once, or pushed up to the remote as separate branches. You're also not limited to just one remote. You can add as many remote repositories as you want!  

Why would you want to have multiple remote repositories? We'll look at this later but briefly, if you are working with multiple developers then you might want to get changes they're working on in their branch(es) into your project before they merge them into the master branch. You might want to do this if you want to test out their change before you decide to implement your changes.  

Another example is if you have a project whose code is hosted on Github but deploys via Git to Heroku. You would have one remote for the `master` and one for the `deployment`.  

`git remote` command will let you manage and interact with remote repositories.  
If you haven't configured a remote repository then this command will display nothing. One caveat to this is if you have cloned a repository. If you have, then your repository will automatically have a remote because it was cloned from the repository at the URL you provided.  

Running `git remote` on a repo that has been cloned from GitHub will output the word `origin`  
The word `origin`, here, is referred to as a "shortname". A shortname is just a variable or a short and easy way to refer to the location (path or url) of the remote repository. A shortname is local to the current repository (as in, your local repository). The word "origin" is the defacto name that's used to refer to the main remote repository. It's possible to rename this to something else, but typically it's left as "origin". It's a lot easier to use just a name like `origin` rather than the entire path to the remote repository.  

If you want to see the full path to the remote repository, then all you have to do is use the `-v` flag: So, `git remote -v` would output something similar to:  
`origin https://github.com/UserName/project-name.git (fetch)`  
`origin https://github.com/UserName/project-name.git (push)`  

## Sending commits to a remote with `git push`  
Before pushing commits to a remote, you have to assign the remote location to a shortname such as `origin` with the `remote` command as described above.  
`git push <remote-shortname> <branch>` the defacto shortname to use is `origin` and the defacto branch is `master`.
`git push origin master` will push all commits in `master` to the remote previously assigned to `origin`.  

## `git pull` vs `git fetch`
`git pull` works the same as `git push` in reverse. The important thing to note is that it is merging the changes automatically after downloading them. This will not work if there have been changes  on the remote further along than local repo. So, for this case and/or just to download the commits without merging them automatically, the command to use is `git fetch`  
`git fetch origin master` will download the new commits from the remote master branch, but will not automatically merge them locally. So you will often want to run a merge command after a fetch command, and then a push command to make the remote and local repos the same.  

## view log info grouped by author
`git shortlog` will display the commit messages and number of commits grouped alphabetically by author.  
adding `-s` will show just the number of commits next to each author name without the commit messages.  
adding `-n` will sort them numerically rather than alphabetically by author.  
`git log --author="author name"` will show all commits made by that author.  

## filter through logs with grep  
`git log --grep="bug"` will show only commits that contain the word `bug`.  
Search is case sensitive so "CSS bug" will not find "css bug".  

## cloning a repository
`git clone "URL"` will make a local copy of the repository linked to. This also creates a connection to the remote using the default shortname `origin`. Keep in mind, then you must be the owner of the repo than you clone in order to push changes to it, but it will let you clone other peoples repos and just not let you push changes. Ideally, you should first fork the repo on github (there is no terminal command to fork) and then clone your own forked copy.  
you can also add a second shortname to the remote of the original repo you forked from.
This shortname is typically called `upstream` instead of `origin` (remember that `origin` points to your own forked copy, while `upstream` should point to the original repo you forked from). You can set this with `git remote add upstream "URL"`  
The purpose of having this second remote is to fetch `git fetch upstream master`, switch to it `git checkout master` and merge in changes from the original repo  `git merge upstream/master` to stay in sync with it as you work. This only updates the local copy, so you would also need to `git push origin master` to sync your forked copy on github.   

## The Rebase Command  
The rebase command can be used to do many powerful things, but can be very dangerous.
In this example we are going to `squash` the last 3 commits into a single commit with a new commit message.  

The `git rebase` command will move commits to have a new base. In the command `git rebase -i HEAD~3`, we're telling Git to use `HEAD~3` as the base where all of the other commits (`HEAD~2`, `HEAD~`1, and `HEAD`) will connect to.  

The `-i` in the command stands for "interactive". You can perform a rebase in a non-interactive mode. While you're learning how to rebase, though, I definitely recommend that you do interactive rebasing.  

It can be a good idea to make a branch called backup or something similar before performing a rebase.  

`git rebase -i HEAD~3` will open your code editor just as it does when expecting a message as with commits. Here it will show the last three commits in reverse order, so the newest will be at the bottom. The default action will be `pick` which as described below in the code editor means it will commit each one. That's not what we want to do. Change `pick` to `s` or `squash` for the bottom and middle commits. It won't work if the top commit is set to `squash` because there is nothing to squash it with. You could leave the top one as `pick`, but we want to change the commit message. So we will set the top commit to `r`. Save and close the code editor to continue the change. This will open a new code editor allowing us to reword the commit message. Do so, then save and close the editor. This will open one last code editor to set the final commit message. Type the commit message, save and close to continue. This will return to the terminal and make the changes. That is it will combine the last three commits into one new commit with a new message.

Instead of using `HEAD~3` to tell it where to base the new commit from, you could also refer to a SHA, branch, or tag.  

## force pushing  
After doing a rebase, the next push will probably fail because github try's to prevent you from accidentally deleting commits. This is a perfect time to use a force push with `git push -f`.

## Other `git rebase` Commands:  
- use `p` or `pick` to keep the commit as is  
- use `r` or `reword` to keep the commit's content but alter the commit message  
- use `e` or `edit` to keep the commit's content but stop before committing so that you can:  
    - add new content or files  
    - remove content or files  
    - alter the content that was going to be committed  
- use `s` or `squash` to combine this commit's changes into the previous commit (the commit above it in the list)  
- use `f` or `fixup` to combine this commit's change into the previous one but drop the commit message  
- use `x` or `exec` to run a shell command  
- use `d` or `drop` to delete the commit  

## When to rebase  
As you've seen, the `git rebase` command is incredibly powerful. It can help you edit commit messages, reorder commits, combine commits, etc. So it truly is a powerhouse of a tool. Now the question becomes "When should you rebase?".  

Whenever you rebase commits, Git will create a new SHA for each commit! This has drastic implications. To Git, the SHA is the identifier for a commit, so a different identifier means it's a different commit, regardless if the content has changed at all.  

So *you should not rebase if you have already pushed the commits you want to rebase.* If you're collaborating with other developers, then they might already be working with the commits you've pushed. If you then use `git rebase` to change things around and then force push the commits, then the other developers will now be out of sync with the remote repository. They will have to do some complicated surgery to their Git repository to get their repo back in a working state...and it might not even be possible for them to do that; they might just have to scrap all of their work and start over with your newly-rebased, force-pushed commits.  
