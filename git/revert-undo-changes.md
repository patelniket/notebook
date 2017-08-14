In this section we will look at how we can revert a file to previous state.

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
