## IPython

%lsmagic

2+10

 _ : last output, __ next to last output, and so on
_+13

; suppresses output
10+20;

! enables shell commands
!pwd

!dir

output from shell stored as a python list
files = !dir 

what is inside {} is evaluated as python
!echo {files[0].upper()} 


from IPython import embed
embed(header='ipython embed')

ipython notebook --script
ipython notebook --pylab=inline

in IPython Notebook: Ctrl+h lists keyboard shortcuts

## Python
```
# scraping-related

#lxml.html (in anaconda)
#html5lib
#beautifulsoup (in anaconda)

#requests (in anaconda)
#urllib2
#mechanize

#xpath?

# anaconda package management
#conda
#conda list 

# python
#python -i filename : runs python in interactive mode, i.e., runs code and leave variables for debugging

# ipython
#ipython -pylab
#ipython -matplotlib

#what is myavi/mlab?

# handling files
#numpy -> loadtt, savetxt, genfromtxt
#csv -> writer, reader
#scipy.io -> loadmat, savemat (MATLAB)

# to get the current working directory
#import os
#os.getcwd()

# to get files in a given directory
#import os
#path = os.getcwd() # for example the current directory
#os.listdir(path)

# regular expression (regex)
import re
m = re.search('(?<=-)\w+', 'spam-egg')
print m.group(0)

filename = 'channela_scheme1_125123_py'
import re
m = re.search('scheme.', filename)
print m.group()

# execute/run a script
#execfile(filename) #filename should include .py
```
