# Version Control using Git & Github

`Version Control`/`Source Control`:

```txt
 - keep track of changes

 - allows two or more developers to work on the same file(s) at the same time

 - compare two versions and see the DIFF

 - rollback to earlier versions when appropriate

 - view changes easly

 - view WHO made the change, WHEN the change was made,and WHY

 - chery pick and merge one change into another when appropriate using integrated tools

```

## Why Git?

```txt

 - Free & open source
 - Distributed
 - Works offline
 - Supports feature branch workflow
 - Community support

```

If you look on Github, `Linux Kernel` alone has `about 25,000 contributors` and `Git` in of itself `about 1,400 contributors`. This should give you a taste of the power of `Git`.

## Check if `Git` is installed

- Type `Bash` as shown below and look for `Git bash`. If you see one, open it

![Git Bash](https://bitbucket.org/ZelalemW/vc-git/raw/master/Resources/check_git.JPG)

- Type `git --version` and press [Enter] key. If you see a version number, then `Git` is installed on your machine.

![Git version](https://bitbucket.org/ZelalemW/vc-git/raw/master/Resources/check_git_version.JPG)


## Install

1. Download and install `git` from https://git-scm.com/downloads - pick for your OS.

2. Verify installation (see above for how)

    ```
    The following tools integrate well with Git and makes life easier when using Git.
    ```

3. Install `KDiff3` from https://sourceforge.net/projects/kdiff3/

4. Install `GitExtensions` from https://sourceforge.net/projects/gitextensions/

5. Configure git settings. This is a one time thing.

    Open `Git Bash` console. You can also do the same from powershell console. But let's stick with `Bash` for now.

    ![Git Bash](https://bitbucket.org/ZelalemW/vc-git/raw/master/Resources/check_git.JPG)

    Then run the following commands, one at a time. Don't forget to replace your name and email address.


    

        git config --global user.name "your full name"

        git config --global user.email "your email address"

    

    ![Git Config](https://bitbucket.org/ZelalemW/vc-git/raw/master/Resources/git_config.JPG)

6. Instead of running one command at a time, let's update `.gitconfig` file which you can find in `C:\Users\<your username>` (eg in my case inside folder: `C:\Users\cleankoder`. Please note: yours will not be `cleankoder`) as shown here:

    ![Git Config file](https://bitbucket.org/ZelalemW/vc-git/raw/master/Resources/git_config_file.JPG)

At this point, it will most likely have only your full name and email configured as :

```

[user]
	name = <your full name provided above>
	email = <your email address provided above>

```

Now, copy and paste the following in that file. Make sure not to override existing setting.

```
[merge]
	tool = kdiff3
[mergetool "kdiff3"]
	path = C:/Program Files (x86)/KDiff3/kdiff3.exe
[diff]
	guitool = kdiff3
[difftool "kdiff3"]
	path = C:/Program Files (x86)/KDiff3/kdiff3.exe
[core]
	editor = \"C:/Program Files (x86)/GitExtensions/GitExtensions.exe\" fileeditor
	autocrlf = true
[credential]
	helper = wincred

```

Also please check if the path to `KDiff3` and `GitExtensions` is the same on your box too. It should be the same but just in case, verify and make correction if necessary.

Save and close.

**Well, that is all there is to it!**

## Sign up for `Github`

1. If you haven't already, please sign up for `Github` from  https://github.com/

2. Create a private repository, `newRepo` or really you can give it any name. Make sure `Add a ReadMe file` is checked and also `Private` is selected.

    ![Gitthub First Repo](https://bitbucket.org/ZelalemW/vc-git/raw/master/Resources/new_repo.JPG)

3. Click on `Create Repository` button.

***Congratulations! You are done setting up `git` and `github`***.

---

Next, we will will learn how to:

```

- clone a repo
- create a new branch
- switch between branchs
- commit our changes
- push our change to remote repo
- create pull request and send out code review
- merge changes to master branch
- handle merge conflict
- stash our change & come back and resume our work later
- and much more

```

---

## **Git**

### 1) ***cloning a repo***

Cloning a repo will `download the project into your computer`. It will also `bring the whole change history` along with it.

1. Copy repository's URL from `Github`

    ![Gitthub Repo URL](https://bitbucket.org/ZelalemW/vc-git/raw/master/Resources/repo_url.JPG)

2. Open `Git Bash` console -> by now, you should know how.
3. Type `git clone <paste your repo URL here>` and press [`Enter`] key.

4. Navigate to the folder containing your newly cloned project and open the `solution` in your favorite `IDE`.

As follows:

![git clone](https://bitbucket.org/ZelalemW/vc-git/raw/master/Resources/git_clone.JPG)

---

Keep the following in mind when using `git`.

**Conceptually** think of having three directories each with its own specific purpose:

1) **`Working dir`**

    - contains `untracked changes`, newly added files, updated or deleted but not staged yet

    - think of this containing changed but not staged files.

    - files modified will be here until you intentionally staged them.

    - Git will not automatically stage it for you. Why? Because it will not know when you are done with your changes.

2) **`Staging dir`**

    - contains `staged changes`

    - think of this a directory holding all changed AND staged files

    - stated files are ready to be committed and be part of repo's change history.

    - changes in this staging dir is ready to be pushed to the remote server (Github in this case)
    - until you commit those staged files, your change is not still part of your repo's change history.

3) **`Remote`**
    - (eg. Github)

    - this is your repository in Github/Gitlab/Bitbucket or Azure Repos

    - The server will takes care storing your source code along with its change history for you.

And also think of files being either `tracked` or `not-tracked`

1) **`Tracked file`**

    - Those are files that Git will know and watch for changes.

    - Anything not intentionally excluded but is within the repositorys folder are tracked.

2) **`Not-tracked`**

    - you can tell Git not to worry about tracking some files/folder.

    - unless explicitly excluded, mr. Git watches everything within the project by default.

    - you explicitly state files not to be tracked by git in .gitignore file

---

### 2) ***Create a new branch***

Everytime you start working on new functionality/story or a bug fix, you need to create a new branch with meaningful name.

1) Open `Git Bash` console

2) Navigate to the folder containing your project

3) Make sure you are on `master` branch first

4) Type `git pull` and press [`Enter`] key. This will bring the latest code from server

5) Type `git checkout -b <your new branch name>` and press [`Enter`] key. Also remember the branch name you just created

![Create new branch](https://bitbucket.org/ZelalemW/vc-git/raw/master/Resources/new_branch.JPG)

Console will switch into the newly created branch. But you can also easly switch to a branch by running `git checkout <the branch you want to switch int0 branch name here>` command.

Note:

![Branching](https://bitbucket.org/ZelalemW/vc-git/raw/master/Resources/branching.JPG)


As you can see, branching gives you and your team mebers to branch out from latest code & `work independently` on their functionality and finally `merge` it back to the main branch (usually called `master`) so everyone else can pick up those changes in their next work.

I am sure you are wondering by now about how two or more developers working on the same project/file(s) won't result in conflicts. Yes, there will be conflicts. But we will see later how to `merge` & `handle the inevitable merge conflict`.

---

### 3. ***Commit changes***

If you don't have sample repo in Github, please create one with a `README` file included. Take a look above on signing up for `Github` section on how to do this.

Once you have the repo, please clone the project to your box. This too was discussed above in `1. Cloning a Repo` section.

Open the project in your favorite editor. `Vistual Studio`, `Visual Studio Code` or really any `IDE` or `Text editor will work just fine for now.

1) create a new branch and call it `my-new-branch`.

2) Remove the whole text from `README.md` file and replace it with just the following

```
    # Projekt Documentationn
```

Just copy paste the above content as is. Spelling error is intentional and leave it as is. We will come back to it later.

3. In your command prompt, run the following command

    ```
    git status
    ```

    This should show you the change status, which files are newly created, which are modified, and which are staged or not.

![Branching](https://bitbucket.org/ZelalemW/vc-git/raw/master/Resources/another-devs-change.JPG)

4. We know, we only have one file at this point anyway but that will change soon. Now, run the following command

    ```
    git add .
    ```

    This command will stage all changed/newly added files to staging dir making it ready for `commit`.

    **Note:**

    The `dot` (**.**) means here `stage all files that is new, modified or deleted`. If you want to stage only very few of them, use the `file name` instead of the `wildcard` character (.)

5. Run `git status` command once again and observe the difference between the output of this vs step 3.

6. Run `git commit -m "init commit"` command

    This command will make your change become part of the project's change history. But your change is still only in your machine and not in `Github` yet. Also the message you will provide should always be short and descriptive.

7. Run `git push` command. This basically will push your change to the remote server.

    **Note:**

    If this is your first `git push` on this branch, `git` will ask you to create the same branch on upstream (`remote`) server. In fact, it will give you the `command` to set it up, simply copy paste and run it.

8. ***Congratulations!***

```
- You just created a new branch,
- made some changes,
- checked status
- staged the changes that need to be commited
- commit your changes
- pushed your commit to your remote repository!
```

Go to `Github` and verify: your branch exists and also the file contains your change.

---

### 4. ***Merge***

While you are working on `feature X`, your fellow developers will be working on different features and bug fixes.

Since developers will be working independently, someone else might merge their change to `master` after you created your branch.

This means `master` has changes that is **not** in your branch. In cases like this, it will be better to `merge` `master` branch into your branch so you have everything on a remote server's master branch plus your change. If you keep this practice, you will have the least possible conflict or no conflict at all when you finally `merge` your branch into `master`. If you wait too long, the diff might be too much and dealing with lots of merge conflict is really not fun.

---

#### ***Handle merge conflict***

To do practice merging, lets consider the following.

1) you are going to create fix the typo in the documentation, for that you got to create a branch `your-typo-docs`

2) While you just started on that work item, another developer started his/her work on say a branch `another-devs-feature-branch`

To use `GitExtension` tool, run `gitex commit` from your console, assuming you did the setup as instructed, it will open `GitExtension` UI which will make:

- viewing newly added, modified or deleted files list easier
- viewing the actual change easier
- you can also easly stage/unstage selected file
- you can easly stage/unstage all files
- provide multi-line comments with bullets for your commit message
- commit or commit & push with a simple button click

![Using GitExtensions](https://bitbucket.org/ZelalemW/vc-git/raw/master/Resources/git-ext-ui.JPG)


But note, that while you were working in your story, the other developer `merged` his/her into the main branch (`master` or `main` or whatever you call it.)

Soon after you are done with your change and code is reviewed too and you are ready to `merge` into the main branch. But since the other developer change is in the main branch, you might likely run into `merge conflict`. Why? well, the other developer might have fixed the typo in the documentation while making their change. You did too and hence now there is a conflict or is it? Let's see.

First, let's push our change to our repo using `GitExtension`

![Another developers change](https://bitbucket.org/ZelalemW/vc-git/raw/master/Resources/another-dev-branch-on-remote.JPG)

Another developer's `pull request` on `Github`
![Pull Request on Github](https://bitbucket.org/ZelalemW/vc-git/raw/master/Resources/pull-request.JPG)

Now, before we `merge` our branch into `master`, lets make sure our branch has everything that is in master including the changes made recently by other developers.

![Merge master into your feature branch](https://bitbucket.org/ZelalemW/vc-git/raw/master/Resources/merge-main-to-branch.JPG)

When there is a `merge conflict` as shown on last image's final console output, you need to run `git mergetool` command. If you follow our setup instruction, this will open `KDiff3` tool.

Remember the following when merging:

- ***base*** - this is the state of the code base at the time when your current branch created

- ***local*** - this means as the name imply the code change in your local branch

- ***remote*** - this is the code that is in the remote server.

You can `cherry pick` and `merge`. You need to pay attention on what you are merging and leaving behind. Make sure you did this on every file with conflict - one file at a time.

Let me stress this again, **merge with care**!
As you can see below, `KDiff3` tool will show you three sections, `base`, `local` and `remote` along with easy to navigate buttons, and easy to edit area. Once you have the conflict on this file resolved, save and exit.
Do the same for every file with merge conflict. Again, merging requires:

- you to identify what is your change
- you to identify the other developer's change
- then make a decision what to take and what to ignore. ATTENTION! ATTENTION! ATTENTION!

![Merge using KDiff3 tool](https://bitbucket.org/ZelalemW/vc-git/raw/master/Resources/merge-tool-with-kdiff3.JPG)

Once all merge conflicts taken care of, you need:

- double check to make sure no more merge conflict
- make sure any new and unrecognized files with extentions **.org** are deleted. When you have a merge conflict, its common for git to generate those. Nuke them out!
- compile your code (if it can be)
- test your code/work to make sure functionality still works
- if there are automated tests, run them to make sure nothing is broken
- commit and push your change

Then, follow the usual procedure to `submit` a `pull request`, and then finally `merge` your change into the `master` branch. Do this merge from `Github` itself.

Our demo repo is finally will contain, the change we made as well as the change other developers made (eg, adding the new script.sql file).

![Final repo's state](https://bitbucket.org/ZelalemW/vc-git/raw/master/Resources/final-repo-state.JPG)

I think, by now, I am sure you saw the power of `Git` and how every developer can work independently on their new feature branch and still syncronizes his/her work back to the main branch.

---

### 5. ***Rebase***

More on this coming up.

---

### 6. ***Stash***

Sometimes, an urgnet work might come in while you are in the middle of a functionality/bug fix. Since, the urgent work is really urgent & can't wait, you need to immediatly jump on it, but you also don't want to abandon the progress you made on the story you were working on. Thanks to `Git`, you have the option to `stash` your progress so you can come back and resume your work later.

Run:

- `git stash -a` or `git stash --all` to stash every changes including those made to ignored files.
- `git stash -u` or `git stash --include-untracked` to stash also untracked files i.e new files in your `working folder` but not staged yet
- `git stash` command and git will save your change on the current branch, making it available to get it back later and resume your work. Note, git stash will **not** stash `unstaged new files` and `ignored` files

![Git Stash](https://bitbucket.org/ZelalemW/vc-git/raw/master/Resources/git-stash.svg)

Source: https://www.atlassian.com

Later, when you are done with your urgent work, you can go back to the previous branch and run `git stash pop` to get back into the last stashed change. If you have more than one stash, you can access them them with `git stash pop stash@{2}` where `2` means the third stash from last one. The last stash being `0`.

But please, unless its really required by urgency, you got to finish the story you started and move on to the next.

---

### 7. ***Squash***

More on this soon.

---

### 8. ***Log***

There are better ways to visualize the `change history` of course but `git log --oneline --decorate  --graph --all`
command can still display in graphical view the change history. Note that, more details can be added but that is a good starting point for quick review.

![Git Stash](https://bitbucket.org/ZelalemW/vc-git/raw/master/Resources/git-log-graphical-on-console.JPG)
---

## Summary of most commonly commands

`git init` => initializes the current directory to be git versioned. You do this to convert a local dir to git tracked. No need to do this on cloned repo

`git clone <url of repo to clone goes here>`

`git checkout -b <your branch name goes here>`  => this creates a new branch with the given name

`git checkout <branch name to switch into>` => this lets you switch from the branch you are on to the name you specified

`git status` => displays list of files that are modifed and tracked/staged or not.

`git add <file name>` => stages the file specified

`git add .` => the `.` here means stage all changed files

`git commit -m "brief and concise message about your change"` => this commits the staged files to git. It records the change as a permanent version or snapshot.

`git push` => this pushs it to remote

`git pull` => gets(downloads) the latest

---

## General Process

I assume you have your bash/powershell/cmdlr shell opened. If not, do so

 1. Be on main branch -- this almost always is `master`

 2. `pull` to get the latest - since you SHOULDN'T be working directly on master branch, there should not be a **merge conflict** here.

 3. If you were working from your branch already, then switch to it and then `merge master` into your branch and **resolve conflicts**( if any - see above for how). Otherwise, if you are going to work on a new feature or bug, then create a new branch

 4. ***Make the necessary changes - whatever that that is.***

 5. When you are done with your changes, then **check status** to see what changed. You never know, some file's ***change could be by accident.***

 6. `Stage` those you would like to `commit/push`. It could be all in most cases but its upto you.

 7. Then `commit` staged changes with `short and descriptive commit message`

 8. `push` your change

 9. Repeat step 1-8 until you are done with your feature or bug fix

 10. When you are done, go to `Github`, create `Pull Request` (`PR)` and send it for code review

 11. Address code review feedback. Some review might require just your response and yet others might require code changes. If it does, resolve all review feedback. If you made lots of change as a result of code review, you might ping the developer(s) who reviewed to take a look at your changes again.

 12. When all review feedback resolved, `merge` your branch into `master`.

**Note**: The above steps will be repeated for any new feature or bug fix that you will be working.

---

Git is powerfull. But as they say, with great power comes great responsibility!
Use it with care. Any time you have to run a command you never run before, check but hey, double check and verify it will `DO NO HARM!`

---

## Excercises - knowing is half the battle, you got to practice to turn it into a skill you can rely on

## Exercise 1

What does the following command do?

```

    1. git clone remote-repo-url

    2. git init

    3. git status

    4. git checkout -b branch-name

    5. git checkout branch-name

    6. git add .

    7. git add file-name

    8. git commit your-commit-message-here

    9. git push

    10. git pull

    11. git merge branch-name

    12. gitex commit

    13. git mergetool

```

**Bonus for Exercise 1**

Considering the below screenshot:

- What will you see in section marked ***`1`*** ?
- What git command will be running when button marked:
  - ***`2`*** is clicked?
  - ***`3`*** is clicked?
  - ***`4`*** is clicked?
  - ***`5`*** is clicked?
- What will you have in section marked `6`?
- What will you have in `lower left section`?

![GitExtensions UI](https://bitbucket.org/ZelalemW/vc-git/raw/master/Resources/gitex-ui.PNG)

## Exercise 2

For the following actions, what command will you be running

1. Pull down repo for the first time from Github to your  machine, so you will have a local copy of it along with its version history

2. Check status of the changes including newly added files, modified or deleted files before staging for commit

3. Stage one-file among those added, modified or deleted

4. Stage all changes

5. Merge (i.e integrate) other developers work that was pushed into master after you pull last time

6. If there are merge conflicts and want to resolve resolve it using the default mergetool you have setup (in our case its KDiff3)

7. Make your staged changes become part of repo's change history.

8. Instead of cloning an existing project from Github, can you convert a project you have into git version controlled? If the answer is yes, what command will you be running?

## Exercie 3

1. Go to your Github and create a new repository.

    - repo name: `my-todos`
    - make it private
    - add readme file.

2. Clone your newly created repo

3. Open your project in your favorite IDE

4. Check if there is any change made. We know there is none, you just cloned.

5. Open your README.md file and change the title to `Todos` &save it.

6. Now go to your command prompt and check status

7. I am sure you see changes, the modified file listed there. Now, when you answer the following, please answer them independetly as if that was the only question asked for #7

        a) Where exactly is the change at this point?

        b) Is it already part of Git's version control history?

        c) Is it available only locally or will you find that change on Github too?

        d) If you attempt to commit, what do you think will happen?

        e) How about if you attempt to push it to Github?

8. By now, you realized that your change is actually not ready for commit and you have to do something about it. Please proceed and stage the file.

9. Check status, I know, I know, just to make sure. Our job requires to be detail oriented and rely on verification instead of assumptions. What do you see? The modiefied file being tracked or not?

10. Now, go make your change become permanent record of change history. Don't forget to give meaningful message

11. Do you think your change made it to Github or perhaps not yet? Keep your answer but then go to Github and verify. What do you see?

12. Push your change to remote (in this case, Github)

13. Go to Github and verify. What do you see for the `README.md` file's content? Did you see your change?

14. Now. get the latest pretending you are working as a team member and hence other developers in your time might have pushed some changes.

15. Now you just started a new feature work and that is to add few `Todo` items. Since you know, you `shouldn't` be working directly on `master` branch, you need to create a `new branch` with meaningful name, lets call it `add-todos`

16. Go to your file and please add the following.

        - revise Github session
        - watch movie
        - read 1 chapter in `blabla` book
        - call `blabla` friend
        - excercise

17. Add new file, call it, `Groceries.md` and add one or more list of groceries (Muzz, Birtukan, stuff like that) and save it.

18. Check status, I am guessing, Git it saying there are 2 files (1 modified, 1 added) but both not tracked (untracked). Is it?

19. Now, be selective and stage Just `README.md` file only.

20. Commit with meaningful message. Feel free to come up with your own message.

21. Stage the newly added file in Q17.

22. Commit your change with meaningful message as well.

23. Push your commits. Since you are working on local branch that don't exist in Github yet, `Git` will ask you to `set upstream origin`, please `run the suggested command`. That will make your newly created branch have a twin brother/sister on Github :)

24. Go to Github and verify. Did you see your changes `with 2 commits` as part of your new branch?

25. Switch into `master` branch

26. Pretend other developers might have pushed changes since the last time you get the latest and hence, it will be wise to to get latest now.

27. Hmmm, take a look modification you made from your branch isn't showing now. But why? Does it mean, its lost?

28. Change the title for `README.md` file from `Todos` to `My Todos`. Add also the following and save it

        - excercise
        - making juice
        - walk for 45 mins

    Note that: From Q25, we are mimicing what other developers might have done while we were busy with our other tasks.

29. Check status

30. Stage the file for commit

31. Commit it with short and precise message that speaks intent of the change made

32. Push your commit(s)

33. Go to Github and verify your change. But don't forget to switch between branches (`master` & `add-todos`) in Github.

34. Pull latest (even if you are the only developer at this point), develop the mindset.

35. Switch into your branch `add-todos`, since that is just your branch, you don't have to pull latest. What you have locally and whats on Github should be the same

36. Now, `merge master branch` into your branch

37. Since we intentionally introduced changes on the same file, on the same lines, I am sure you will run into `merge conflicts` on one `README.md` file. Is it or all went well?

38. Open your merge tool to resolve merge conflicts. At this point, when the `KDiff3 tool` opens, it will show you `4 main sections`
    - Base
    - Local
    - Remote
    - Lower section (this is not a label of course.)

    a) Which section holds the change you made as part of your feature branch?

    b) Which one represents the code change since you branch out and change made by other developers (which in this particular instance you but on a master branch)

    c) And which one represents the code that your branch was based on just when you create the branch

    d) Now do the actual merging. At this point, you got to `chery pick` what to take and what to leave behind. I would say, take both sides except, leave `walk for 45 mins` and instead take `excercise`. Save and close KDiff. If there is another conflict on a different file. Do this until all issues on the file as well as on ALL files that have conflicts are resolved. In this case, you only have one file with conflict and i say, you are one lucky fella

39. You can now start using `Gitextension` tool you setup. Run `gitex commit` and it will popup.
    - Stage the file
    - reset `.orig` file please. Just right click and reset it. Or if you prefer, run `git clean -f` on your command prompt. Either way, will knock out this unwanted file that `Git` created because of the conflict.
    - On lower right section of gitextentions, write a message `merge from master` and click on `commit & push` button

40. Go to Github and verify that your branch should now have the changes made by other developers too.

41. Since you are done with this feature branch you have been working on, create a `Pull Request` in `Github` and `send it for code review`

42. Run `git log --oneline --graph --decorate --all` to see what the branching looks like at this point.

**Congratulations!**

**Happy coding!**
