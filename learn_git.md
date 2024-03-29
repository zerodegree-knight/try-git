

## Clone the Repository

To make your own local copy of the repository you would like to contribute to, let's first open up a terminal window.

We'll use the git clone command along with the URL that points to your fork of the repository.

This URL will be similar to the URL above, except now it will end with .git. In the NetBox example above, the URL will look like this:

https://github.com/your-username/netbox.git

You can alternatively copy the URL by using the green "Clone or download" button from your repository page that you just forked from the original repository page. Once you click the button, you'll be able to copy the URL by clicking the binder button next to the URL:

Once we have the URL, we're ready to clone the repository. To do this, we'll combine the git clone command with the repository URL from the command line in a terminal window:

    git clone https://github.com/your-username/repository.git

Now that we have a local copy of the code, we can move on to creating a new branch on which to work with the code.
#Create a New Branch

Whenever you work on a collaborative project, you and other programmers contributing to the repository will have different ideas for new features or fixes at once. Some of these new features will not take significant time to implement, but some of them will be ongoing. Because of this, it is important to branch the repository so that you are able to manage the workflow, isolate your code, and control what features make it back to the main branch of the project repository.

The default main branch of a project repository is usually called the master branch. A common best practice is to consider anything on the master branch as being deployable for others to use at any time.

When creating a branch, it is very important that you create your new branch off of the master branch. You should also make sure that your branch name is a descriptive one. Rather than calling it my-branch, you should go with frontend-hook-migration or fix-documentation-typos instead.

To create our branch, from our terminal window, let's change our directory so that we are working in the directory of the repository. Be sure to use the actual name of the repository (such as netbox) to change into that directory.

## cd repository

Now, we'll create our new branch with the git branch command. Make sure you name it descriptively so that others working on the project understand what you are working on.

    git branch new-branch

Now that our new branch is created, we can switch to make sure that we are working on that branch by using the git checkout command:

    git checkout new-branch

Once you enter the git checkout command, you will receive the following output:

##Output

Switched to branch 'new-branch'

Alternatively, you can condense the above two commands, creating and switching to a new branch, with the following command and -b flag:

    git checkout -b new-branch

If you want to switch back to master, you'll use the checkout command with the name of the master branch:

    git checkout master

The checkout command will allow you to switch between multiple branches, so you can potentially work on multiple features at once.

At this point, you can now modify existing files or add new files to the project on your own branch.
Make Changes Locally

Once you have modified existing files or added new files to the project, you can add them to your local repository, which we can do with the git add command. Let's add the -A flag to add all changes that we have made:

    git add -A

Next, we'll want to record the changes that we made to the repository with the git commit command.

The commit message is an important aspect of your code contribution; it helps the other contributors fully understand the change you have made, why you made it, and how significant it is. Additionally, commit messages provide a historical record of the changes for the project at large, helping future contributors along the way.

If we have a very short message, we can record that with the -m flag and the message in quotes:

    git commit -m "Fixed documentation typos"

But, unless it is a very minor change, we will more than likely want to include a lengthier commit message so that our collaborators are fully up to speed with our contribution. To record this larger message, we will run the git commit command which will open the default text editor:

    git commit

If you would like to configure your default text editor, you can do so with the git config command, and set nano as the default editor, for example:

    git config --global core.editor "nano"

Or vim:

    git config --global core.editor "vim"

After running the git commit command, depending on the default text editor you're using, your terminal window should display a document ready for you to edit that will look similar to this:

GNU nano 2.0.6 File: �sername/repository/.git/COMMIT_EDITMSG

Please enter the commit message for your changes. Lines starting with '#' will be ignored, and an empty message aborts the commit. On branch new-branch Your branch is up-to-date with 'origin/new-branch'.

Changes to be committed: modified: new-feature.py

Underneath the introductory comments, you should add the commit message to the text file.

To write a useful commit message, you should include a summary on the first line that is around 50 characters long. Under this, and broken up into digestible sections, you should include a description that states the reason you made this change, how the code works, and additional information that will contextualize and clarify it for others to review the work when merging it. Try to be as helpful and proactive as possible to ensure that those maintaining the project are able to fully understand your contribution.

Once you have saved and exited the commit message text file, you can verify what git will be committing with the following command:

    git status

Depending on the changes that you have made, you will receive output that looks something like this:

Output

On branch new-branch Your branch is ahead of 'origin/new-branch' by 1 commit. (use "git push" to publish your local commits) nothing to commit, working directory clean

At this point you can use the git push command to push the changes to the current branch of your forked repository:

    git push --set-upstream origin new-branch

The command will provide you with output to let you know of the progress, and it will look similar to the following:

Output

Counting objects: 3, done. Delta compression using up to 4 threads. Compressing objects: 100% (2/2), done. Writing objects: 100% (3/3), 336 bytes | 0 bytes/s, done. Total 3 (delta 0), reused 0 (delta 0) To https://github.com/your-username /respository .git a1f29a6..79c0e80 new-branch -&gt; new-branch Branch new-branch set up to track remote branch new-branch from origin.

You can now navigate to the forked repository on your GitHub webpage and toggle to the branch you just pushed to see the changes you have made in-browser.

At this point, it is possible to make a pull request to the original repository, but if you have not already done so, you'll want to make sure that your local repository is up-to-date with the upstream repository.
Update Local Repository

While you are working on a project alongside other contributors, it is important for you to keep your local repository up-to-date with the project as you don't want to make a pull request for code that will cause conflicts. To keep your local copy of the code base updated, you'll need to sync changes.

We'll first go over configuring a remote for the fork, then syncing the fork.

Configure a Remote for the Fork

Remote repositories make it possible for you to collaborate with others on a Git project. Each remote repository is a version of the project that is hosted on the Internet or a network you have access to. Each remote repository should be accessible to you as either read-only or read-write, depending on your user privileges.

In order to be able to sync changes you make in a fork with the original repository you're working with, you need to configure a remote that references the upstream repository. You should set up the remote to the upstream repository only once.

Let's first check which remote servers you have configured. The git remote command will list whatever remote repository you have already specified, so if you cloned your repository as we did above, you'll at least see the origin repository, which is the default name given by Git for the cloned directory.

From the directory of the repository in our terminal window, let's use the git remote command along with the -v flag to display the URLs that Git has stored along with the relevant remote shortnames (as in "origin"):

    git remote -v

Since we cloned a repository, our output should look similar to this:

Output

origin https://github.com/your-username/forked-repository.git (fetch) origin https://github.com/your-username/forked-repository.git (push)

If you have previously set up more than one remote, the git remote -v command will provide a list of all of them.

Next, we'll specify a new remote upstream repository for us to sync with the fork. This will be the original repository that we forked from. We'll do this with the git remote add command.

    git remote add upstream https://github.com/riginal-owner-username/riginal-repository.git

In this example, upstream is the shortname we have supplied for the remote repository since in terms of Git, "upstream" refers to the repository that we cloned from. If we want to add a remote pointer to the repository of a collaborator, we may want to provide that collaborator's username or a shortened nickname for the short name.

We can verify that our remote pointer to the upstream repository was properly added by using the git remote -v command again from the repository directory:

    git remote -v

Output

origin https://github.com/your-username/forked-repository.git (fetch) origin https://github.com/your-username/forked-repository.git (push) upstream https://github.com/original-owner-username/original-repository.git (fetch) upstream https://github.com/original-owner-username/original-repository.git (push)

Now you can refer to upstream on the command line instead of writing the entire URL, and you are ready to sync your fork with the original repository.

Sync the Fork

Once we have configured a remote that references the upstream and original repository on GitHub, we are ready to sync our fork of the repository to keep it up-to-date.

To sync our fork, from the directory of our local repository in a terminal window, we'll use the git fetchcommand to fetch the branches along with their respective commits from the upstream repository. Since we used the shortname "upstream" to refer to the upstream repository, we'll pass that to the command:

    git fetch upstream

Depending on how many changes have been made since we forked the repository, your output may be different, and may include a few lines on counting, compressing, and unpacking objects. Your output will end similarly to the following lines, but may vary depending on how many branches are part of the project:

Output

From https://github.com/original-owner-username/original-repository * [new branch] master -&gt; upstream/master

Now, commits to the master branch will be stored in a local branch called upstream/master.

Let's switch to the local master branch of our repository:

    git checkout master

Output

Switched to branch 'master'

We'll now merge any changes that were made in the original repository's master branch, that we will access through our local upstream/master branch, with our local master branch:

    git merge upstream/master

The output here will vary, but it will begin with Updating if changes have been made, or Already up-to-date. if no changes have been made since you forked the repository.

Your fork's master branch is now in sync with the upstream repository, and any local changes you made were not lost.

Depending on your own workflow and the amount of time you spend on making changes, you can sync your fork with the upstream code of the original repository as many times as it makes sense for you. But you should certainly sync your fork right before making a pull request to make sure you don't contribute conflicting code.

