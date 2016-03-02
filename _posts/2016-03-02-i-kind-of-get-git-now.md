---
layout: post
title: "Well, I Kind of Get Git Now"
date: 2016-03-02
---

Welcome to the inaugural post of this blog. Time will tell if I post more. This was mainly a lesson in git pages to see if I could get it working. Seems I have. At any rate, this post features the kind of tutorial on starting with git that I wish I'd have been able to find when I was first starting out. 

I know for a fact that there are other tutorials which are both more concise and succinct. The point here isn't to be concise or succinct. The point is to slowly step through some very simple git processes in order to gain a rudimentary understanding in git.

git is set up in repositories. Whether these repositories are local or remote is immaterial. You can do the same things in any location as long as you have the software to manage it. A repository contains all the content for your project. Sometimes that project is just a single feature and other times it is an entire site or application. In our case, we’re talking about sites.

## Installing git

You can download git piecemeal or you can download a third party command line tool with git included. 

git:
[https://git-scm.com/downloads](https://git-scm.com/downloads)

cmder:
[http://cmder.net/](http://cmder.net/)

With cmder, be sure to include git in the package by selecting the full install. For both git and cmder, there are extensive documentation you can use to find commands you need to do your work. There are GUI options for git. I do not use these, so their use would have to be self-taught for now.

#Initiating a New Local git Repository

Create or navigate to the folder in which you would like to create a git repository. If you know you will be pulling a repository (repo) from a remote location, feel free to leave the folder empty.
Open command line and navigate to your folder. Tab to autocomplete
Type:  git init  
You should get a message saying the repo was initialized.
Type:  dir 
You shouldn’t see anything.
Open the folder using the normal Windows GUI (Windows Explorer).
You should see a folder called .git which is a hidden folder. This is where all the files full of your settings and different versions of your files are located. Do not touch this folder.
If this is a new repository for a new project, you may want to consider a .gitignore file. This file will tell git to ignore certain files or folders in a project. Good examples of a files to ignore are .htaccess or settings.php. Basically, anything pertaining to a specific server should be avoided. For Drupal sites, it also may be a good idea to ignore entire folders, such as those devoted to content (documents and such).
https://git-scm.com/docs/gitignore 
Type:  git status
You should get a response telling you that you’re on the master branch. We’ll discuss Branches later.

Connecting To a Remote Repository
Type: git remote
Nothing should show.
Get the URL for your remote repository. A vendor should supply any URLs you need and also provide you with credentials for accessing the files. On Github, a repository’s URL can be found on the main repo page. 
Example:  https://github.com/ny/opwdd.ny.gov
To create a connection to the example Repo, we would type:  
git remote github https://github.com/ny/opwdd.ny.gov.git
The “github” portion of the command just gives a name to this connection, which can be used any time after it has been created. We could have called it “Marvin” or “poop” if we wanted.
Type: git remote
You should see the remote connection in there. This means a repo can have multiple remote connections. This allows you to disseminate your repo anywhere you want, whether with Github, Acquia, or anywhre that accepts git repos.
Type:  git pull github master
This tells git to pull all the files at your github location, but from the branch called “master”.
You will be prompted for your username and password. 
It may take some time to download the files
When it is done, you may notice in cmder that it now tells you which branch you’re working from (in this case, master).
Type:  dir
You should see a listing of all the files that were in the repository’s main branch.
Feel free to go in through windows explorer and look at the .gitignore file if one exists to see what that looks like.

Working With Git 
Go back to your command line interface. Type: git checkout -b demo
The “-b” is a parameter. Most commands have different parameters which are detailed in the git documentation.
Cmder will show you are in a new branch. You can also type git status
Completely close out your command window.
Open a new command window and navigate to your repo’s folder.
You will note that the branch you are in persists even when the window is closed.
Navigate to your folder in Windows Explorer and create a new folder called “demo_yourname” where “yourname” is your first name. Then, inside that folder, create a text file called “demo.txt”
In that text file, write “Hello world!”
In your command line, type:  git status
You will note that your new folder has been detected by git as something with changes. These files are NOT being tracked as an actual change, though. It will not automatically do this.
In this way, you can ignore changes in other parts of your project while focusing on changes in other sections.
Type:  git diff HEAD
You will see no changes listed.
Type:  git add .
The “.” tells git to add all changes. You could have also typed:
git add demo_yourname
In cmder, note that the branch name has turned red, denoting that there are changes on the branch. git status will tell you what has changed.
Type:  git diff HEAD
You will see your changes printed and it will look like a patch file
It is actually possible to use the diff command to output actual patch files using different options
Type:  git commit -m “Initial creation of my demo file.”
The text inside the quotes can be anything you want describing the work you did.
Type: git checkout master
You are now on the master branch
Type:  dir
The /demo_yourname folder should be gone.  This is because we have switched to the master branch which has none of the changes we made on the demo branch.
Type: git checkout demo
The /demo_yourname folder should have returned.
Type: git checkout master one more time.
Type: git merge demo
This takes all the committed changes from your demo branch and makes them to the files on the master branch.
Type:  dir
You should see your files now. Master and demo should now be identical.
Type: git checkout demo
In your demo.txt file, add another line, perhaps “Hello to you too!”
In your command line, type these commands, noting what happens each time:
git status 
git add .
git diff HEAD
git commit -m “Added a line to the demo.txt”
You wouldn’t normally commit after every little change, of course. This is just for demonstration.
git checkout master
Note that, in your text editor, the line you added to demo.txt has probably been removed!
git merge demo
And it probably has now returned, because you merged the changes from the demo branch.



Working with the Remote
You’ll eventually want to push your changes to a remote repository, whether it’s in the ITS github or Acquia. When you do your push, you do so by name.
Navigate to the remote repository on the Github website. You will see that your demo folder is not up there. Example: https://github.com/ny/opwdd.ny.gov 
In git, checkout the demo branch:  git checkout demo
Type:  git push github HEAD
This will push all the changes in your current branch whatever it is.
You could push a specific branch by putting that branch’s name in place of “HEAD”.
Check the remote repository again in your browser. 
Click the branches drop-down and select the demo branch.
You will see the files listed change, adding your demo folder. If you switch back to master, you will not see it because you did not push master.
In git, switch to the master branch:   git checkout master
Type:  git push
You will get an error. 
Type the command git suggests: git push --set-upstream github master
You will be asked for your credentials.
Now refresh the master branch list in github. Your demo folder should be visible.


Rolling Back
In command line, checkout demo again and commit another change with a third line to your document, “Goodbye!” Make the commit message “Said goodbye.”
git checkout demo
Add line to document
git add .
git commit -m “Said goodbye.”
git push github demo
But wait! You didn’t want to say goodbye. You need to roll back to a previous commit. 
List your last 3 commits with this command:  git log -3 | cat
The “git log” lists your commits. The “-3” tells git to only list the last three. the “ | cat” tells git not to use vi to scroll through the commits. Instead, it will just spit them all out relatively instantaneously.
If you want to set | cat as the default so you don’t have to type it all the time, use this command to set the global:
git config --global core.pager cat
There are a lot of global defaults you can set in git. Check the documentation on how to do this.
Type:  git revert ##################################### --no-edit
The # represents the commit number from your log that you’d like to get rid of. The “--no-edit” spares us going into vim to edit a message. You may wish to set a different text editor for such things, or learn vim. -_-
You don’t have to put the full #. The editor will know what to do if you give the first few numbers.
If you are using cmdr, you can select the text with your left mouse button and dragging. Then, if you right-click, the text will insert automatically wherever your cursor is. You don’t use ctrl+c and ctrl+v in cmder.
If you want, you can check your log for the revert commit and actually revert the revert.
There are LOTS of ways to roll back changes, some of them VERY complicated. I haven’t even come close to mastering this stuff yet.
Merge your changes with master
git checkout master
git merge demo

Deleting Files
Time to get rid of our demo folder. We don’t want that hanging around in the repo.
Type: git checkout demo
Go into windows explorer and delete the demo folder.
Type: git status
Git should tell you that a file has been deleted
Type: git rm demo_yourname -r
Where “demo_yourname” is the name of your demo folder.
This stages the folder for deletion
There are lots of shortcuts for adding and removing files. Check out the documentation for more info.
Commit and push. Now you can see the difference between master  and 





Well. Finally got around to putting this old website together. Neat thing about it - powered by [Jekyll](http://jekyllrb.com) and I can use Markdown to author my posts. It actually is a lot easier than I thought it was going to be.
