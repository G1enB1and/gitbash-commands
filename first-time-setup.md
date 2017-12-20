# First Time Git Configuration
Before you can start using Git, you need to configure it.
Run each of the following lines on the command line to make sure everything is set up.

// sets up Git with your name  
`git config --global user.name "Glen Bland"`
  
// sets up Git with your email  
`git config --global user.email "glen.bland.81@gmail.com"`
  
// makes sure that Git output is colored  
`git config --global color.ui auto`
  
// displays the original state in a conflict   
`git config --global merge.conflictstyle diff3`  
  
`git config --list`  
  
## Git & Code Editor  
The last step of configuration is to get Git working with your code editor.
Below are three of the most popular code editors. If you use a different editor,
then do a quick search on Google for "associate X text editor with Git" 
(replace the X with the name of your code editor).  
  
### Atom Editor Setup  
`git config --global core.editor "atom --wait"`  

### Sublime Text Setup  
`git config --global core.editor "'C:/Program Files/Sublime Text 2/sublime_text.exe' -n -w"`  

### VSCode Setup  
`git config --global core.editor "code --wait"`  
