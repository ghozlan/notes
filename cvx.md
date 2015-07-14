
#CVX

## Download and install 

Mac (on-campus computer center machines)

Run in shell
```
export CVX_DL=http://web.cvxr.com/cvx/cvx-maci64.zip # download link
cd ~
curl $CVX_DL > cvx-package.zip
unzip cvx-package.zip
```

Open matlab (in shell):
```
export MATLAB_PREFIX=/Applications//MATLAB_R2014a.app
export PATH=$PATH:$MATLAB_PREFIX/bin
matlab --no-desktop
```
or open matlab with GUI.

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

## Use

Example
```
m = 20; n = 10; p = 4;
A = randn(m,n); b = randn(m,1);
C = randn(p,n); d = randn(p,1); e = rand;
cvx_begin
    variable x(n)
    minimize( norm( A * x - b, 2 ) )
    subject to
        C * x == d
        norm( x, Inf ) <= e
cvx_end
```

http://cvxr.com/cvx/

#CVXPY

## Download and install

Ubuntu

Run in shell
```
sudo apt-get update
sudo apt-get install -y libatlas-base-dev gfortran #Install ATLAS and gfortran (needed for SCS).
sudo apt-get install -y python-dev
sudo apt-get install -y python-pip
sudo apt-get install -y python-numpy python-scipy
#sudo pip install cvxpy  #install for all users
pip install --user cvxpy #install locally
sudo apt-get install python-nose
nosetests cvxpy #Test the installation with nose
```

## Use

Example

```
from cvxpy import *
import numpy

# Problem data.
m = 30
n = 20
numpy.random.seed(1)
A = numpy.random.randn(m, n)
b = numpy.random.randn(m)

# Construct the problem.
x = Variable(n)
objective = Minimize(sum_squares(A*x - b))
constraints = [0 <= x, x <= 1]
prob = Problem(objective, constraints)

# The optimal objective is returned by prob.solve().
result = prob.solve()
# The optimal value for x is stored in x.value.
print x.value
# The optimal Lagrange multiplier for a constraint
# is stored in constraint.dual_value.
print constraints[0].dual_value
```

http://www.cvxpy.org/en/latest/

http://stanford.edu/~boyd/software.html

#CVXOPT?
