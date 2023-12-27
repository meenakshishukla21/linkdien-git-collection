# Git commands

## 1. Git Configuration

- System Level

```
git config --system
```

- User Level

```
git config --global
```

- Project Level

```
git config
```

- Setting a few configurations

```
git config --global user.name "Your name"
git config --global user.email "Your email"
```

- To see all your configs at one place

```
git config --list
```

- To list only global/local configs

```
git config --list --global
git config --list --local
```

- To look at each individual configuration e.g your name

```
git config user.name
```

- To have a look at your `.gitconfig` file

```
code ~/.gitconfig
```

- To set VSCode as your default editor while using git.

```
git config --global core.editor "code --wait"
```

- To add colors to git messages(red, green for successful commits).

```
git config --global color.ui true
```

- To set default branch name as main

```
git config --global init.defaultbranch main
```

- To get help and see options for a particular git command.

```
For eg: git help <command-name>
> git help log
OR
> man git-log
```

## 2. Git-completion

- [Visit this](https://github.com/git/git/tree/master/contrib/completion) to have a complete look.
- Add a `.git-completion.bash` script to auto complete git commands.

```
> cd ~
> curl -o .git-completion.bash https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash
```

- Open `.bashrc` file and add these lines to the script.

```
# Tab-completions for git-branch names
if [ -f ~/.git-completion.bash ]; then
    . ~/.git-completion.bash
fi
```

## 3. Useful commands

- Initialize a project to use git.

```
git init
```

- To see git directory which keeps track of changes in your repo.

```
> cd .git
> ls -a
```

- To add all the changes made.

```
git add -A
```

- To commit the changes you made to the repository.

```
git commit -am "Your-commit-message"
```

- Commit message best practices.

1. Short single-line summary(less than 50 chars).
2. Use present tense instead of past tense.
3. Message may start with shorthand followed by the org. For eg: [css, js], "bugfix: ", "#38045 - ".
4. After one blank line, you can add decriptive message.

- To view the commits that have been made to a project.

```
git log
```

- To see more options you get with git log

```
git help log
```

- Few of the useful options with `git log`.

```
> Shows recent 5 commits.
git log -n 5

> Show commits from/until a particular date.
git log --since=2020-01-01
git log --until=2020-01-01

> Show commits of a particular author.
git log --author="Saurabh"

> Search for a commit message using grep(globally searching for regular expressions).
git log --grep="Message you want to search"
```

- A look at how the above options can be combined as well.

```
> Command that will output the last two commits that happened before September 10, 2020.
git log --until=2020-09-10 -n 2

> Output the log for all of Karen's commits labeled "refactor" during March 2019.
git log --since=2019-03-01 --until=2019-03-31 --author="Karen" --grep="refactor"
```

- To get the SHA value of the commit where HEAD pointer points to.

```
> cat .git/HEAD

This spits out a refs address. Copy that. For eg: `ref: refs/heads/main`

> cat .git/refs/heads/main
This will output the SHA value of the commit where HEAD points to.
```

```
NOTE: The .git/HEAD file indicates the branch HEAD currently points to, and the contents of the file will contain the SHA of that branch's HEAD. If you checkout another branch, the contents of .git/refs/heads/new will not change, but the .git/HEAD contents will.
```

## 4. Get going with Git Commands

- To check your current status(asking you to add the changes to staging index or git repository(committing).

```
> git status
```

- To selectively add files to your staging area(meaning to track the changes)

```
> git add <fileName1> <fileName2>...
```

- To see the differences between files before `staging`. OR . To view the changes in the `working directory`.(differences btw working tree and staging index)

```
git diff
```

- To view the changes in the `staging area`(differences btw repository and staging tree).

```
git diff --staged

OR

git diff --cached
```

- When you `delete` the files, it also get tracked. So, you need to add after deleting to the staging area and commit. In order to delete and move that change to staging area use `git rm` :

```
git rm <file_to_delete.txt>
git commit -m "file_to_delete deleted"
```

- To track `moved/renamed` file. (Renames the file and stage this change to the staging tree simultaneously)

```
git mv initial_file_name.txt final_file_name.txt
git commit -m "Rename a file"
```

## 5. Undo Changes

- Undo/Discard `working directory` changes meaning, say you made a change to a file `index.html` and you have not staged it yet and you want to discard the changes made to this file.

```
git checkout -- index.html
```

- Undo the changes made to the staging tree. (Means the changes are added to staging area but not committed and we want to restore the changes.) `OR` Unstage the changes made to the staging tree.

```
git reset HEAD <fileName1>...<fileNameN>
```

- To amend/edit the last commit you made. For eg: Your recent commit should also include one more edit. So, you made the `edit to the file and staged it`. Now :

```
git commit --amend -m "Merge this commit with prev commit"
```

```
NOTE: The previous commit will be deleted and the changes made to previous commit + changes made to recent commit are committed under the message "Merge this commit with prev commit".
```

- To see any commit(means what all changes it did). Copy it's SHA value and write:

```
git show <SHA-value>
```

- Similarly, to change the commit message to the recent(last) commit.

```
git commit --amend -m "Old changes with new message"
```

```
NOTE: Working of amend:
Take whatever is the old commit(to which HEAD is pointing to), bring it back down to staging area, add whatever changing has into it, and then recommit it.
```

- To revert a commit(undo changes) done in older commits. Copy the older commit `SHA-value` and run:

```
git revert <SHA-value>

It opens up the editor to see the new message and the previous commit SHA. Save the file. See, now using git log that revert has been applied to the older commit.
```

```
> NOTE: That's why make the changes atomic. So, you can revert the chnages you want to rather than reverting 50 lines of code.
```

- To remove untracked files in the working tree.

```
git clean -f

NOTE: git clean -n ,for preview of the files to be deleted.
```

## 6. Ignore files

- Create `.gitignore` file in the root of your repo and put the lists of files you want to ignore. For eg: `logs/*.txt` will ignore all text files in the `logs/` directory.
- Put all those files in `.gitignore` which is not necessary to keep track of. For eg: `DS_Store`, `*.zip`.
- What to ignore: `compiled source code`, `packages and compressed files`, `logs and databases`, `user uploaded assets(images, PDFs, videos)`.
- A collection of [gitignore templates](https://github.com/github/gitignore#a-collection-of-gitignore-templates).
- To setup a global `.gitignore` file. Follow [this](https://gist.github.com/asksaurabh/0a1dbb1f2b242dbf601e44c469fab0d0#11-setup-global-gitignore-file).
- `.gitignore` ignores the files that are untracked. To ignore files that are already tracking: Say you were tracking `db_config.txt` and now you don't want to track it anymore.

```
Step 1: git rm --cached db_config.txt
Step 2: Open .gitignore file and write db_config.txt in it.
Step 3: git commit -m "Stop tracking changes to db_config file"
```

- To list all the files and directories that are tracked by git.

```
git ls-tree HEAD
```

- By default, git ignores to track empty directories. To track these, a simple way is to make a invisible dot file inside empty directory. Conventionally we call this `.gitkeep`. For eg: Let's say we want to track a empty `resources` directory.

```
> mkdir resources
> touch resources/.gitkeep
> git add -A
```

## 7. Navigating the Commit Tree

- To reference previous commits. Copy the `SHA-value`(usually 4 or more characters) and :

```
git show <SHA-VALUE>

OR

> If you want to reference head.
git show HEAD
```

- To find the ancestry(parent, grandparents..) of the commit. Usage of (`^` or `~(generation number)`).

```
> For parents
git show <SHA>^
git show HEAD^
git show HEAD~1

> For grandparents
git show HEAD^^
git show HEAD~2
```

- To list the contents of a tree object ie. `"tree-ish" or SHA-Value or HEAD`.

```
git ls-tree HEAD

> It lists the contents of commit that HEAD is pointing to. Use git help ls-tree for options.
```

```
Usage:  Lists the contents of parent of HEAD
> git ls-tree HEAD^
```

- To filter the commit log.

```
> Filter by number of commits.
git log 3

> Filter by date.
git log --since=2022-01-01 --until=2022-01-31
git log --until="3 days ago"

> Filter by author.
git log --author="John"

> Search by commit message/regex.
git log --grep="Initial"

> Log every commit between two SHA values.
git log SHA1..SHA2
git log a5637bf..HEAD

> Show every commit which changed a specific file. For eg: index.htm. It helps you to see only those commits which affected index.html file.

git log index.html
```

- Format the commit log. (Use it for better display of metadata related to a particular commit)

```
git log -p

> Shows all the previous commits with their change sets.
```

- To show the statistics with each commit.

```
git log --stat
```

- To change the format of the git log

```
git log --format=short

> Available: oneline, short, medium(default), full, fuller, email, raw
```

- IMP: To show the graph of the previous commits(shows branches and all also).

```
git log --graph

Also try: git log --graph --all --oneline --decorate
```

## 8. Branching

- Be careful when you are creating a new branch, check what branch are you currently on. `Creating a branch will create branch from current branch you are on`.

- To see all the existing branches. It also shows the currently checked out branch via `*`

```
git branch
```

- To create a new branch.

```
git branch <branch-name>
```

- To switch(checkout) between branches.

```
git checkout <branch-name>
```

- To create and simultaneously switch to a new branch.

```
git checkout -b <new-branch-name>
```

- How to `switch/checkout when you have uncommitted changes`:

```
1. You cannot switch if uncommitted changes in working directory conflict.
2. You can switch if uncommitted changes in working directory could be applied without conflict.
3. You can switch if files are not being tracked.
```

```
How to checkout in these conditions then:
1. Commit the changes  to the current branch and then checkout
2. Remove the changes, checkout the file now.
3. stash the changes.
```

- To compare two branches to see what difference they have:

```
git diff branchName1..branchName2
```

- To find out what other branches have all of their commits merged into this branch already: For eg: Suppose I'm at `shorten-title` branch and I want to see what other branches have all of their changes merged into shorten-title branch.

```
git branch --merged
```

```
> Output:
  lengthy-title
  main
* shorten-title

This means all of the commits that are in main and lengthy-title branch are their in shorten-title branch.
```

- Similarly, to check what all branches commits are not merged in current branch

```
git branch --no-merged
```

- To rename the branch name (be careful to rename before you start sharing it with other people/branch).

```
> If you want to change the name of current branch:
git branch -m <new-branch-name>

> If you want to change the name of any random branch:
git branch -m <old-branch-name> <new-branch-name>
```

- To delete a branch, first need to checkout to a branch other than you want to delete(because you can't be on a branch you are trying to delete). Now:

```
> To delete the branch which have no commits or is merged.
git branch -d <branchName>

> To delete the branch which have commits and you don't even want to merge it also.
git branch -D <branchName>
```

## 9. Reset Branches

- Moves HEAD pointer to a specific commit. (changing the files in staging index/working driectory).
- Three types of reset: soft, mixed and hard
- Soft reset: Moves the HEAD pointer to a specified commit but it does not changes the staging index and the working directory. For eg: If you moved to commit A in time, and it has commit B and C above it. So, All those changes in commit B and C moves to `staging index` ready to be `committed` again.

```
git reset --soft <tree-ish>
```

- Mixed reset: Moves the HEAD pointer but it changes the staging index to match the repository. It doesn't change the working directory. This is a default choice of `git reset` if you don't specify any option. For eg: If you moved to commit A in time, and it has commit B and C above it. So, All those changes in commit B and C moves to `working directory` ready to be `staged` again.

```
git reset --mixed <tree-ish>
```

- Hard reset: Moves the HEAD pointer. It changes the staging index and the working directory to match the repository. It returns to an old stage and `discards` all the code changes. Used to permanently undo commits. Mainly used for making one branch look like another completely.

```
git reset --hard <tree-ish>
```

## 10. Merge Branches

- First move to the branch where you want the merge the changes into(generally main).

```
git checkout main
```

- Now, see the differences between the current branch(say main) amd the branch you want to merge with(say test).

```
git diff main..test
```

- To merge the test branch into the main branch(currently you are here).

```
git merge <branch-name-you-want-to-merge>

> Here: git merge test
```

- NOTE: ALWAYS run merges with a `clean working directory`. Things becomes complicated if you have unstaged changes in working directory while doing merges. SO, either `stash or commit the changes` in the `working directory` before running merge.

- Two types of merges: Fast forward and True merge.
- Fast forward merge is when the test branch is just an extension of main branch, hence it can easily be moved in-line with main branch. Hence, when merged no new commit to merge is made. Git just moved the commits to main branch.
- True merge is when we have additional commits in main from the point where new branch was made to test and when you want to merge test back to main, we need to have another commit which joins the two branches together.

- Conflict occurs when we have two changes in the same line in two different commits.
- Three ways to resolve merge: abort merge, resolve the conflicts manually, use a merge tool.
- Abort merge

```
git merge --abort
```

- To resolve a merge manually:
- To see the differences in the current branch.

```
git diff --color-words main..<branch-you-are-merging-with>
```

- Make the changes manually, then stage the changes, then commit without a message, message shows up in editor, save and exit.

- How to reduce merge conflicts?
- Keep merging main branch into your feature branch. This is called `tracking`. We are merging changes in feature-branch from main branch to keep feature-branch up-to-date with main to reduce merge conflicts.
- You can use `git reset --hard <tree-ish>` to undo the merge.

## 11. Stash changes

- It's not a part of the working directory, staging index or repository. It's a separate are of git, where we save things for later.
- Say you have made some edits to your file in a particular branch but have not staged it yet. Now, you want to checkout to another branch. You can't do that. You either need to commit the changes or stash it.

```
git stash save "your-stash-message"
```

- Stash by default does not include untracked files, as it doesn't produce a conflict when switching branches. To stash untracked files, use:

```
--include-untracked option of git stash
```

- View stash

```
git stash list
```

- View a particular stash commit

```
git stash show stash@{index-you-want-from-list}
```

- To view the contents of a particular stash commit

```
git stash show -p stash@{0}
```

- You can view the stash anywhere. It's independent of the branch you made the stash to.

- You can retrieve the stash changes at any branch you want. So, first you need to decide which branch you need to retrieve the stashed changes and to retrieve them and remove from stash:

```
git stash pop [stash@{index}]
```

- To retrieve the changes but not delete them from stash.

```
git stash apply [stash@{index}]
```

- To clear a particular commit in stash

```
git stash drop [stash@{index}]
```

- To clear the whole stash

```
git stash clear
```

## 12. Set up a Remote

- Remote repos are hosted by servers over a network and allows easy collaboration. Push local repo changes to the remote.
- origin/[branch-name] is a branch on our local machine that references the remote server branch and it always try to stay in sync with that remote branch.
- When you fetch(pull) changes, the remote main sync up with the local origin/main branch it doesn't show changes in the local main branch. To sync local main we need to merge.
- To check list of remotes

```
git remote
```

- To check git configs

```
cat .git/config
```

- To remove a remote(let's say origin)

```
git remove rm origin
```

- To create a new remote branch

```
git push -u origin <branch-you-want-to-push>
```

- To show remote branches

```
git branch -r
```

- To show all local/remote branches

```
git branch -a
```

- To clone a repository

```
git clone <https-link> [project-name]
```

## 13. Collaborate with a Remote

- To push to a remote repository if it is already set to tracking(-u flag)

```
git push
```

- Had the remote branch set up to non tracking, then you need to specify which branch you are pushing to.

```
git push origin main
```

-To fetch changes from remote repository

```
git fetch
```

- NOTE: This fetch makes the local origin/main branch in sync with the remote main branch, but the `local main branch is still behind`.

- NOTE: Fetch before you start work. Fetch before you push. Fetch before you go offline. Fetch often.

- To merge in fetched changes, First see diff between local main and local reference to origin/main(which is tracking remote main).

```
git diff --color-words origin/main..main
```

- Now, standing on the local main, perform the merge

```
git merge origin/main
```

- Two step process: `git fetch(to see what comes down) + git merge`
- To do both steps at once. Use:

```
git pull
```

- Let's say we have two remote branches called origin/test and origin/main. If someone clones repo, it gets only main as local repo. To get test as a local repo.

```
git branch test origin/test

> This tells to create a local branch test based of of origin/test

OR: Do it in one step
git checkout -b test origin/test
```

- If you want to push to an updated remote branch, remember to first fetch to get all the remote changes, then merge, then push.

- To delete a remote branch(eg: test)

```
> git push origin :test

OR

> git push origin --delete test
```

- To collaborate, first identify the problem you will work on, then fork the project, make changes and push it to your own remote fork, then raise a PR.

- NOTE: Before pushing: FETCH MERGE then PUSH
- NOTE: Before start working: FETCH MERGE then start working.

- Add an alias:

```
git config --global alias.st status
```

## Collboration with Teams

- Go to the orgs repo(eg: facebook/react) on which you want to contribute. Fork it.
- Now you have your own copy(eg: asksaurabh/react).
- Clone your own repo(asksaurabh/react) into your local system. This automatically sets your `origin` to be your own forked remote copy.
- See all the remotes: `git remote -v`
- Setup org's repo as an upstream from which you can pull recent changes.

```
git remote add upstream <ORG-GITHUB-SSH-CLONE-LINK>
```

- To get updates from upstream

```
git pull upstream master
```

- Now our individual fork doesn't have these updates. So, push these changes to our own forked copy.

```
git push origin master
```

## NOTES

- Remember to work in the feature branch for doing any changes.

```
git checkout -b <New-branch-name>
```

- Add and commit the changes in this feature branch.
- Push this feature branch upto the github.

```
git push -u origin <New-branch-name>
```

- Now, to create a PR, go to your own forked GitHub repo `asksaurabh/react`, go to the corresponding feature-branch 'New-branch-name' and create a PR. Click on Compare and pull request.
- See the relationship created: Merge into facebook/master from asksaurabh/New-feature-branch-name.
- Add comments and create the PR.
- Once merged, delete the new feature branch locally and its remote reference.

```
git branch -d <New-Branch-Name>
```
