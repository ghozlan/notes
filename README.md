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
      
# Bit Bucket
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
  - GitHub Pages
  - Git LaTeX report?

# Cloud/Online IDEs
- Koding
- Nitrous, free plan requires phone number (24.5.15)
      - Free tier: 2 hours/day + 10 GB storage. See pricing [here](https://pro.nitrous.io/pricing/#free)!
      - File transfer: possible through FileZilla (need public/private keys).
      - How to access GitHub in nitrous?
- Cloud 9 
- Codenvy?
- PythonAnywhere
      - Free tier: 100 CPU-seconds/day, 512 MB disk space and 2 consoles (bash or python). A CPU-second is one second of full-power usage on a High Frequency Intel Xeon E5-2670 v2 (Ivy Bridge) Processor (one CPU core on an Amazon AWS m3.xlarge instance). See pricing [here](https://www.pythonanywhere.com/pricing/)!
      - Python packages numpy, scipy, matplotlib are already installed
      - File transfer: upload/download is possible through the web interface. No public/private keys are required which makes the process simple.
      - No GUI?
   
# More
- [x] bitbucket (created account on 29.5.15)
- [ ] mapreduce in python
- [ ] spark (berkeley stack) in python
- [ ] mysql/python
- [x] kaggle (signed-up 4.6.15)

# Kaggle
