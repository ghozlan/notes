# GitHub
- [ ] rename repo (and its effect on local copy): https://help.github.com/articles/renaming-a-repository/
- [x] how to create a to-do list: https://help.github.com/articles/writing-on-github/#task-lists
- [ ] how to get absolute url up to the repo main level
- [ ] remove a commit? an intermediate commit
- [ ] branch vs fork
- [x] get a list of remote aliases: check [remote "..."] entries in
      
           
            cat .git/config
           
- [x] upload a repo created on local server to GitHub:
      1. Push an existing repository from the command line

            git remote add origin https://github.com/ghozlan/<repo-name>.git
            git push -u origin master
                  
      2. Use "Publish Repository" in GitHub desktop
      
# Bit Bucket
- [ ] links in bitbucket (markdown?)
- [x] import a git repo from github into bitbucket: possible through Repositories> Import repository
- [ ] upload a git repo from local machine into bitbucket

# Python
- [ ] figure name
- [ ] figure position and size
- [ ] figure fontsize in xlabel, ylabel
- [ ] figure fontsize in legend
- [x] regex: how to get x and y in pattern channelx_schemey_...? (29.5.12)

      wrote some notes about in another file in the repo
- [x] regex: re.complile vs re.search (29.5.15) 

      `re.compile(pattern).search(string)` is functionally equivalent to `re.search(pattern, string)`
- [ ] regex: re.compile().sub(,)
- [ ] regex: re.compile().split()
- [x] profiler ( 28.5.15)
- [x] line profiler ( 28.5.15)
- [x] memory profiler ( 28.5.15)

# MATLAB
  - Dynamic field indexing in structures

# Amazon Web Services (AWS)
## Elastic Cloud Compute (EC2)
- [x] Install packages on Ubuntu (27.5.15)
   - [x] python (already installed)
   - [x] pip / easy_install
   - [x] virtualenv
   - [x] numpy
   - [x] scipy
   - [x] matplotlib 
- [ ] Create custom Amazon Machine Image (AMI) with packages above

# Other
  - PyCharm 
    - Lint
    - Fix import error
  - Cloud IDE
    - Koding
    - Nitrous, free plan requires phone number (24.5.15)
    - Cloud 9 
    - Codenvy?
  - GitHub Pages
  - Git LaTeX report?
   
# More
- [x] bitbucket (created account on 29.5.15)
- [ ] mapreduce in python
- [ ] spark (berkeley stack) in python
- [ ] mysql/python
- [ ] kaggle
