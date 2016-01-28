# Git Cheat Sheets

* http://www.git-tower.com/blog/git-cheat-sheet/
* https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf

# Git

* Check if remote is ahead
```
git remote -v update
git status -uno
#git show-branch *master #show commits in all branches whose names end in master
git pull
```
(http://stackoverflow.com/questions/3258243/git-check-if-pull-needed)

* Stage a file for deletion
```
git rm <filename>
git rm --cached <filename> #delete from repo but keep file in filesystem
```
(http://stackoverflow.com/questions/12373733/staging-deleted-files)

* delete/remove/undo most recent commit(s)

```
git reset --hard <commit-id>
#If you already pushed it, you will need to do a force push to get rid of it
git push origin HEAD --force
```
(http://stackoverflow.com/questions/1338728/delete-commits-from-a-branch-in-git)

* clone a specific files and/or subdirectories of repo (called sparse checkout). this is useful if, for example, there is a directory for source code, a directory for builds/executables and a directory for help/documentation. One might want to check out only the source code (to avoid download/upload of big files).

```
git init
git remote add origin <url>
#tell git that a part of the repo will be checked out 
git config core.sparseCheckout true
#define which files/folders to check out
echo "some/dir/" >> .git/info/sparse-checkout
git pull origin master
```
(http://stackoverflow.com/questions/600079/is-there-any-way-to-clone-a-git-repositorys-sub-directory-only/600189#600189)

# GitHub
- [ ] rename repo (and its effect on local copy): https://help.github.com/articles/renaming-a-repository/
- [x] how to create a to-do list: https://help.github.com/articles/writing-on-github/#task-lists
- [ ] how to get absolute url up to the repo main level
- [ ] remove a commit? an intermediate commit
- [ ] branch vs fork
- [x] get a list of remote aliases: check [remote "..."] entries in
      
           
            cat .git/config
           
- [x] upload a repo created on local server to GitHub:
      1. Push an existing repository from the command line (the commands are given by GitHub after a new repo is created)

            git remote add origin https://github.com/ghozlan/<repo-name>.git
            git push -u origin master
                  
      2. Use "Publish Repository" in GitHub desktop
 
- [x] commit part of file (hunk)
      ```
      git add --patch filename.ext
      ```
      See [this](http://stackoverflow.com/questions/1085162/commit-only-part-of-a-file-in-git)
      
- [x] revert one file (not all the files) to the version of a specific commit (20.6.15)
      This could be done by checking out only that file from the commit you want:
      
      ```
      git checkout <commit> <filename>
      ```
      
      Note: To see the commits, use
      
      ```
      git log --oneline
      ```

      The output looks like:
      ```
      ...
      30db46e MU-MIMO Uplink
      0f37b40 Updated mimo.py
      4b8b164 SU-MIMO 2x2
      8a37f64 Initial commit
      ```
- [x] list all branches

      ```
      git branch --all --verbose
      ```
- [x] list current config (user.name, user.email, ...etc)
      ```
      git config --list
      ```
      
      to set user.name and user.email
      ```
      git config --global user.name "ghozlan"
      git config --global user.email "hassan.ghozlan@gmail.com"
      ```

# Bit Bucket
- [x] make a link to the latest file (without specifying the commit)
      
      Instead of this
      ```
      https://bitbucket.org/ghozlan/wltv-output/raw/ea8c5c6debc72450a61b5193d595ad1054583ebf/html/multilayer_script.html
      ```
      use
      ```
      https://bitbucket.org/ghozlan/wltv-output/raw/master/html/multilayer_script.html
      ```
      
      This is useful, for example, when wanting to use htmlpreview
      ```
      https://htmlpreview.github.io/?=url-to-html
      ```
 
- [ ] links in bitbucket (markdown?)
- [x] import a git repo from github into bitbucket: possible through Repositories> Import repository
- [x] upload a git repo from local machine into bitbucket
      1.  Push an existing repository from the command line (the commands are given by Bitbucket after a new repo is created)
            
            cd /path/to/my/repo
            git remote add origin https://ghozlan@bitbucket.org/ghozlan/<repo-name>.git
            git push -u origin --all # pushes up the repo and its refs for the first time
            git push -u origin --tags # pushes up any tags
      2. SourceTree: 
            * Repository> Add Remote> Add. 
            * Remote name: <alias> and URL / Path: https://ghozlan@bitbucket.org/ghozlan/<repo-name>.git
            * Push

Pros:
* Offers private repos.

Cons:
* No markdown preview. You can preview the README.md file though.
* No check boxes in markdown (github has it, but I think it is not standard markdown)
