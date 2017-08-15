##Reverting file in git repository to previous state

When you do git checkout ```commit_id``` you will checkout the commit in a detached ```HEAD``` state where the ```HEAD``` will be pointing to the ```commit_id```.

This will be experimental read only mode and no changes will happen to your repository. You can use ```git checkout -b <new-branch-name>``` to take any changes in this state to the new-branch-name.

![git-checkout-commit](/assets/git-co-ci.png)

Then if you commit any thing is this state and checkout any other branch without ```-b``` option it will warn you as below:

![git-checkout-warning](/assets/git-co-warn.png)

Now lets take a look at ```git checkout <commit_id> <filename>```
Any changes you make here will also reflect in you repository.

![git-checkout-commit-file](/assets/git-co-ci-file.png)

If you decide to revert the above checkout and fall back to the previous state. You can run below command to checkout ```HEAD``` back to the ```<filename>``` instead of ```<commit_id>```.

![git-co-head-file](/assets/git-co-head-file.png)

But let's take a look at what needs to be done if you really what to revert the changes back to the ```<commit_id>```.

Going back to previous state. This already adds file to the staging area, so we don't need to run ```git add```

![git-co-ci-cofile](/assets/git-co-ci-cofile.png)

Let's commit our change.
And that is how a file can be reverted back to it's previous commit (state) while working within one branch and not in detached ```HEAD``` state.

![git-log](/assets/git-log.png)

In summary, ```git checkout <commit_id> <filename>``` will checkout a previous version of a file. This converts the file that resides in the __current working directory__ into an exact copy of the file from the ```<commit_id>``` and adds it in __stating__ area. Checking out old file does affect the current state of your repo. You can then recommit a new snapshot of this file as you would commit any other change.

## Reverting and Undoing changes in Git Repo

```git revert HEAD``` command can be used to revert the changes and add the change as a new commit, instead of just removing the commit from history.

This prevents git from loosing history

![git-co-intro](/assets/git-co-intro.png)

![git-revert-head](/assets/git-revert-head.png)

Another way to revert changes is a git reset command.
```git reset <filename>``` command un-stages the file but leaves the working directory unchanged

![git-unstage](/assets/git-unstage.png)

![git-reset](/assets/git-reset.png)

If you want to un-stage all files then you could simply use git reset command without specifying the file name.
 
To un-stage changes as well remove the changes from working directory you can use ```git reset --hard```

This command will not only remove the files from staging but will also undo changes in working directory.
 
To reset back to a particular commit_id you could use ```git reset <commit_id>``` command. This will reset your changes in git commit history back to that particular commit id and you will have the relevant commit related files unchanged in he working directory. By default this is a ```-mixed``` reset.
 
You can also perform a hard commit reset with ```git reset --hard <commit_id>``` command back to the commit_id and it will not only remove the commits from the commit history but it will also remove the relevant changes from the files.
 
To clean the untracked files in the working directory you can use ```git clean``` command. One caution is that this command is not undoable.
Run ```git clean -n``` command to do a dry run without actually removing the untracked files

Most of the times git clean is used in addition to ```git reset --hard``` command to reset history and remove all the files from working directory as well.

You can use ```git clean -xf``` command to force-delete untracked files, even those mentioned in the ```.gitignore``` file (that’s what ```-x``` option is for). This can be handy to clean the directory after a build (binary .class files as an example) and even ```.DS_Store``` files on a mac before releasing the project repo.
