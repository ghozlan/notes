
#CVX

Download and install CVX on mac machine (on-campus computer center machines)

Run in shell
```
export CVX_DL=http://web.cvxr.com/cvx/cvx-maci64.zip # download link
cd ~
curl $CVX_DL > cvx-package.zip
unzip cvx-package.zip

export MATLAB_PREFIX=/Applications//MATLAB_R2014a.app
export PATH=$PATH:$MATLAB_PREFIX/bin
matlab --no-desktop
```

Then run in matlab shell
```
cd ~/cvx
cvx_setup
```

You will get these instructions
```
---------------------------------------------------------------------------
NOTE: the MATLAB path has been changed to point to the CVX distribution. To
use CVX without having to re-run CVX_SETUP every time MATLAB starts, you
will need to save this path permanently. This script attempted to do this
for you, but failed---likely due to UNIX permissions restrictions.
To solve the problem, create a new file
    /Users/ghozlan/Documents/MATLAB/startup.m
containing the following line:
    run /Users/ghozlan/cvx/cvx_startup.m
Please consult the MATLAB documentation for more information about the
startup.m file and its proper placement and usage.
---------------------------------------------------------------------------
```

http://cvxr.com/cvx/doc/install.html
