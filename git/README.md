# Git in terminal

[Download Github Desktop here.](https://desktop.github.com/)

---

## Push & pull

cd into the project folder and do a `git pull`.

```
$ git pull
```

Pushing your code; add the files you want to push, make a commit and then push the commit to the branch you're working on.

```
$ git add .
```

Above command will add all files in the project assuming you're at root directory.

```
$ git commit -m "This is my commit message"
```

The `-m` flag is short for message, commit messages should be descriptive but not nessessarily detailed!

```
$ git push
```

And we just made a push from our terminal.

---
<br>
<br>

## Branches

Ok, you have a repository set up, you're in the project folder in the terminal.<br>
Lets have a look at branches.

```
$ git branch
```

This will list all branches we have on our local PC.<br>
If you at some point have other branches in the git but they're not visible here, don't worry we will get to that.

```
$ git branch myNewBranch
```

The above command creates a new branch with the name `myNewBranch`.<br>
It creates a copy of the branch we are currently in, so if we are in `master`/`main` branch then we just made a copy of that branch.<br>
But if you run `git branch` you'll see we are still in the same branch, lets change.

```
$ git switch myNewBranch
```

or

```
$ git checkout myNewBranch
```

Both commands above will take you to the new branch, but there are some differences between these commands and because of that I always use `checkout`.

`git switch` will in this case work as expected, but if the branch you want to change to isn't on your local PC then this command won't work.

`git checkout` does exactly the same as `switch`, but in the case where you don't have the branch locally, this will pull that branch and change to it. `git branch -a` to view all branches including remote branches.

```
main branch
|
|
|\
| \
|  \
|   | * myNewBranch
v   v
```

If you think of git branches as a timeline like illustrated above, then it might make more sense.<br>
The asterisk(`*`) is just an indicator of what branch we are on.

---
<br>
<br>

## Detached HEAD

This is where it gets a bit more complicated.

```
main branch
|
|
|\
| \
|  \
|   X * myNewBranch (initial commit)
|   |
|   |
|   X - a new commit
|   |
v   v
```

In the illustration above we have made a new branch, change to it and made 2 commits; the initial commit and a new commit with some changes to our code.<br>
But what if we wanted to go back to our inital commit? This is where `detached HEAD` comes in.<br>

Each commit gets a unique ID, and we can use this ID to hop back into old commits.<br>

```
$ git log
```

If we open the log we get an overview of commits in the current branch.<br>
The commit ID's looks like this: `cf40d8fcfe70343c4f36b1ef356dbd033e93c4d3`.<br>
You can also take a look at the commits on github.com.

```
$ git checkout cf40d8fcfe70343c4f36b1ef356dbd033e93c4d3
```

I just went back to a previous commit, again I have to use `checkout` because `switch` won't work as this is not a branch.

```
Note: switching to 'cf40d8fcfe70343c4f36b1ef356dbd033e93c4d3'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>
```

You can also do the following to make a new branch from detached HEAD.

```
$ git branch someNewBranch
$ git checkout someNewBranch
```

Then we just make a new branch while we are in detached HEAD state, our new branch is a copy of this commit and we can then continue editing in our new branch.

---
<br>
<br>

## Merge

Merging can be difficult and confusing, depending on the size of the project and how many developers that are working on it. Doing smaller merges more often rather than a few large can make this process easier.

In this case I will use the `terminal` and `Visual Studio Code` do to a merge.

```
A  Tmp  B   main
|   |   |   |
\   |   /   |
 \  |  /    |
  \ | /     |
   \|/      |
    X       |
    |       |
    \       |
     \      |
      \     |
       \    |
        \   |
         \  |
          \ |
           \|
            X - Tmp merged into main
            |
            v
```

`A Branch` has work we want to merge into main.<br>
`B Branch` also has work we want implement into main.

We then change to `main`, make a new branch which I have called `Tmp`(temporary).<br>
`Tmp` is now a copy of `main`, we then change to our new temporary branch.

```
$ git checkout main
$ git branch Tmp
$ git checkout Tmp
$ git branch

  main
  A
  B
* Tmp
```

We will now merge both `A` and `B` into `Tmp`. Make sure you are in Tmp branch!

```
$ git merge A
```

I can now open the VS Code editor, view the `Source Control` tab and accept all incoming changes.<br>
Everything in branch A that is new will be added to Tmp(which is a copy of main of course).

```
$ git merge B
```

We are still in Tmp and we now merged the B branch on top of the A branch.<br>
We want to accept the incoming changes we want to keep but at the same time make sure we don't mess with the new code from branch A. This can be difficult when 2 developers or more have been working on the same files(which we always do).<br>
This is where comments in code can come in handy.

Assuming everything went fine and all code have been tested and checked, then we want to merge our Tmp branch into main.

```
$ git checkout main
$ git merge Tmp
```

Then accept all incoming changes(we just want to replace main with Tmp basically).<br>
After merging Tmp into main we can then delete the Tmp branch to avoid clutter in our git.<br>
At a later point we can also delete A and B branches as well to tidy up our git.

Have another look at the illustration above after reading all this, and it should make more sense now.

> Problems merging A and B into Tmp? Or just made a huge mess?

Simply delete the Tmp branch, make a new one and try again.

```
$ git checkout main
$ git branch -d Tmp
$ git branch Tmp
$ git checkout Tmp
...
```

Change to main, then delete the Tmp and then we start over...

---
<br>
<br>

## For Unity development

[Official Unity Collab](https://scholarslab.lib.virginia.edu/blog/sharing-unity-project/)

> To begin, make sure you have created a free Unity account and are logged in. The free account allows you to build a team of up to three collaborators

or

[How to use Github with Unity](https://unity.github.com/)
