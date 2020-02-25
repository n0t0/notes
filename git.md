### GitHub
git help
git help <command>
git help glossary

### Available Commands 
git help -a

### Guides
git help -g 

### Initialize a project 
git init <dir>
git add . # adding files 
git checkout — <filename> # cleaning changes to a file
git reset HEAD <filename> # cleaning added file 
git rm — cached <filename> # fresh repo only
git commit -m “Message!”
git commit -a -m “Message!” 
git status 

### Logging 
git log 
git log —oneline
git log —oneline —decorate # showing the branch 
git log -n 3
git log <filename>

git blame -p <file>

### Diff uncommitted modified files
git diff —cached <filename>
git diff HEAD <filename>

### List Branches 
git branch

### Create a Branch
git branch <branch_name>

### switch branches 
git checkout <branch_name> 

### Merging Branches 
git merge <branch_name> 

### Deleting a Local Branch
git branch -d <branch_name>

### Deleting a Remote Branch
git push origin --delete "developer.update.configmap" 

### Checking Remote Repositories 
git remote -v 

### Adding Remote Repository 
git remote add origin <link>

### Pushing to Remote Repository
git push -u origin master 

### Pulling to a Local Directory 
git pull

### Cloning and Forking 
- first fork the explored project 
git clone <link> 

### Checking GitHub rep for a Changes 
git diff origin/master 

### Lits Tags
git show-refs --tags -d  