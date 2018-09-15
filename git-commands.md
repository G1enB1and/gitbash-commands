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
`git commit` opens the code editor associated with bash, shows you what branch your on and the files being commited and prompts you to add a message to the commit.  
  
## git diff  
`git diff`  

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
