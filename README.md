

Background/knowledge:
- why to use git
    - Able to store everything remotely, in case you're on another PC, or your PC dies
    - If you ever got stuck where you made a bunch of changes, but now your program doesn't work, and you can't get it back to how it was before? Git means you can revert to a previous point in time when it was working. 
    - Can have a copy of the codebase with only your changes, so only your work is there until merged back in
    - Gives a more structured way for many developers to work on the same code base. Nobody accidentally but quietly overwrites someone's work. 
    - Easier to review changes before those changes go into the code base. 
    - Everything is saved, so there's a complete history of work, and you can "go back in time" if needed. 
- Important things NOT to do
    - do NOT commit credentials to the repo. If you do, change them immediately. 
- Theory
    - The "why to use it" mentioned above
    - Branching (small branches that are relatively short lived. 2 month old branches with lots of changes is a bad idea)
    - Remote and local repo (github is a place to store a git repo, but is one of many)
    - Commits, and staging
    - Pulling and pushing from/to remote repos
    - Locking the main branch, to ensure all merges to main happen through Pull Requests where other developers can review them first


Practical experience:
- Use git --version to check the version
- Use git init to create a repo
    - Create a git repo with a single file name "temp.py"
    - locate the .git folder in the root directory, where all the "git" stuff is stored
- Delete the .git folder to delete the repo
    - Decide that you don't want this to be a repo, and delete the repo, keeping all the files. 
- git clone
    - Clone a given open source repo from github, gitlab, or alternative
        - Run the command correctly
        - Before hitting enter on the command, be able to tell that the clone will create a folder with the same name as the repo. e.g., git clone my-repo creates a my-repo/ folder. 
    - Delete the repo by simply deleting the entire folder
- Create a repository on a free hosting site of your choice, such as Github or Gitlab
    - Choose the options needed to not initialize the repo with any files. Once created, most empty repos will give you a "cheat sheet" of commands for various situations, such as starting a new repo, pushing up an existing repo, etc. 
    - Locate the button which gives you the url to clone the repo
    - Clone the repo you have created using the url
- git status, add, commit -m, git restore, git reset
    - Use git status and locate the branch you're on, as well as the portion showing whether files have changed and need to be committed
    - Add a new file with two lines of text
    - Use git status and again locate the branch, as well as this new "untracked" file. 
    - Use git add <file_name> to "stage" that file. That is, to add it to the files to be committed
    - Use git status to see that this file is now listed in green as a file to be committed
    - Use git restore --staged <file_name> to unstage the file, then use git status to confirm this change
    - Use git add . to add all files so that the file is staged once again, and use git status to confirm it's staged
    - Use git reset to unstage everything that is currently staged, confirming this has happened with git status. Then use git add . again to restage one last time
    - Use git commit -m "My first commit" to commit the changes, with the message "My first commit" attached to your commit
    - Use git log, and you will see this commit
- git diff and git diff --staged (should caution that these can *sometimes* be a little weird compared to what's expected, but still usually good)
    - Add a new line of text to the file and save
    - Use git status to view what files are modified but not staged(newlines count, so you may see blank lines with + or - to represent those)
    - Use git diff to see a "diff" view, showing what changed in the file to be committed. You should see the new line with a + next to it
    - Delete one of the two previous existing lines and save
    - Use git diff to see that there is now a - by the line which was removed
    - Use git add to stage these changes. 
    - Use git diff and note that the changes in that file no longer appear, because git diff shows unstaged changes by default
    - Use git diff --staged to show those changes. This is a good check to do before you commit
    - Commit the changes with a message of your choice
- git pull, push
    - Use git push to push your new commits from your local repo to the remote one you created
    - Go to the web interface for your repo, and see that your changes are now there
    - These changes won't be on anyone else's machines, but when they do git pull, these changes to the branch will be pulled down
- checkout new branch, merge branch. (Work should be done on feature branches in small units, not the main branch)
    - Create and delete a branch locally
        - Use git checkout -b my-feature to create (and be switched to) a new branch. 
        - Use git branch to show all branches, with an * next to the branch that you're on. git status will also show you. 
        - Use git checkout main to switch back to main, and git branch to confirm this switch. 
        - Use git branch -D my-feature to delete the feature branch
    - Using the website you chose, create a new branch on the website named my-feature. If prompted, select to branch off of main. 
    - On your PC, use git pull. This will indicate that a new branch named my-feature exists
    - Use git checkout my-feature to swap to the branch you have created, and git branch to confirm you're on that branch
    - Add a couple new lines of text to your file
    - Add and commit these changes
    - git push to push your changes to the remote repo
    - Click on the branch you've pushed on the website, and locate the "create new pull request" button. 
    - Locate the tab which shows the diff between main and my-feature, to verify that everything looks as expected
    - Use the website's button to merge, checking the "delete branch after merging" button if available. Otherwise, delete the feature branch since it's now unnecessary. 
- Use .gitignore file
    - Each line will identify a file or directory that git should ignore. Perhaps because you're storing a file with credentials, perhaps because it's IDE settings, perhaps it's a sqlite database file. 
    - Note that because it starts with a . it will be "hidden" on some file systems, so it may appear absent at first glance. 
    - Create a file called settings.json. Use git status to see that this new file is present
    - Create a file named ".gitignore"
    - Add "settings.json" on the first line
    - Use git status to verify that settings.json has disappeared from the output
    - commit this new .gitignore file
- resolve merge conflicts
    - Create two new branches off main, named feature-one and feature-two. These must both be created at the same time. 
    - On feature-one, add one line at the end of the file saying "I am adding a feature from feature-one". 
    - Commit and push these changes. 
    - Checkout the main branch, and use git pull to ensure it's updated. 
    - Checkout feature-one again, and use git merge main, to merge main into feature-one. This will merge all changes in main into feature-one, if there are any. 
    - There shouldn't be, so you can push feature-one, and merge it into main. 
    - On feature-two, add one line at the end as before, but with the line reading "I am adding a feature from feature-two". Commit and push these changes. 
    - Again, checkout main and use git pull to ensure it's updated. 
    - Checkout feature-two, and use git merge main, to merge main into the branch you're on (feature-two)
    - Git will inform you that there is a merge conflict, because the same line was changed in two separate branches, and you must decide how to handle it. 
    - If using a basic text editor, the conflict will have some conspicuous <<<<<<<<>>>>>>>> symbols around the whole conflict and a line of ====== between the two conflicting portions. This is just indicator text, so don't be afraid of it; you'll just delete it. 
    - Choose how you would like the file to look. You can keep both lines, you can change it to read "I am adding a feature from both feature-one and feature-two", or whatever makes sense to you. 
    - Delete the indicator text, add and commit the file, then push the changes. 
    - Merge feature-two into main, now that the merge conflict has been resolved. 
- git log and git log --oneline to see change log
    - Checkout the main branch if not on it, and use git pull to ensure it's updated
    - use git log to show detailed output about each commit. Locate:
        - The hash of each commit
        - The author
        - The date
        - The commit message
    - use git log --oneline to condense the output onto one line

- git stash, git stash list, git stash pop, git stash push with message, compare stash with current state of repo
- check remote with git remote -v
- git blame
- tags

- cherry pick?
- revert?
- git config for setting name and email and such?
- README.md, it's purpose in most git repos, and some basic markdown?
