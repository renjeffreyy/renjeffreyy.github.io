# Git

## Creating Branches

- Branches are for when you want to work on your code but you want to keep changes seperate from your master branch
- they are good for when you want to create new features
- mainly how teams collaborate on projects together
- you push and commit your changes on the branch to local and remote repositories to save your work
- Once you are finished working on your feature, you can make a pull request to asks admins or team members to merge your pull request to the master branch
- if there are no question,comments, or change requests they will merge the code. if there are concerns you just edit your branch and make another pull request

### Terminal commands for branches

how to check all branches in your local repo

`$ git branch`

How to create a new branch

`$ git branch your_branch_name`

How to go to the branch you just created (or any other branch)

`$ git checkout you_branch_name`

You can use one command to create your branch and go to it

`$ git checkout -b your_branch_name`
