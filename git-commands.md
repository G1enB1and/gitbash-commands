#git commands  

## To start a new local empty repository:  
Before you can make commits or do anything else with a git repository, the  
repository needs to actually exist.  
To create a new repository with Git, we'll use the `git init` command.  

`git init`  //  create a new, empty repository in the current directory.  

The `init` subcommand is short for "initialize", which is helpful because it's  
the command that will do all of the initial setup of a repository.  

## To clone an existing git repository:  
`git clone` // download a copy of an existing repository to the current working  
// directory. Current working directory must not already be a git repository.  

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

## Other git commands:  
`git status` // displays information such as which files are in which states.  
