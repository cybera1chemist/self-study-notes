# Course2: Version Control

## Module3 Working with Git

### Git and Github

#### Branches:

git checkout -B branchName // create a new branch (if dosen't exst) and swith to this branch

See current branch: `git branch`

Branches are independent of each other. Changes to the new branch will not affect main branch or other branches.

#### Remote:

git init // Create a new repository (add a .git file) (local)

git remote -v // 

git remote add origion git@github.com:{urlbalabala.git}

#### Workflow:

Developer should add features in a new branch first, then push it into main branch.

`git commit -m 'The message you want to write.'`

#### HEAD:

First `cd .git`, then `cat /refs/heads/main`: returns a hash code

`cat .git/HEAD`: return which branch the HEAD is pointing to.

#### Diff: Find the differences

`git diff HEAD README.md`: returns the changes in this file

`git log --pretty=oneline`: show logs

`git diff main new_branch`: show differences between 2 branches

#### Blame: Find who made the changes

`git blame Feature.js`: returns all changes of this file

`git blame -L 5,15 setup.py`:  only returns line5-line15

### Create a Repository with Forking

Difference between branching and forking:

Forking creates a new repository entirely.

(clone other's repository into your account)

就像在伯克利写作业的时候一样！
