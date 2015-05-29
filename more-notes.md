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

## Regular Expressions (RegEx)
search

```
#%% Regular Expressions (a.k.a RegEx, regex, regexp)
import re
filename = "channela_scheme1_125123_py"
nonmatch_filename = "redbud.tree"

#%% No match case
m = re.search(r"channel._scheme.", nonmatch_filename)
if m:
    print "match"
else:
    print "no match"    # no match

#%% Finding a match
m = re.search(r"channel._scheme.", filename)
if m:
    print m.group(0)    # channela_scheme1
    print m.groups()    # empty list
    print m.groupdict() # empty dict
else:
    print "no match"
    
#%% Extracting the channel index and the scheme index (using subexpressions)
m = re.search(r"channel(.)_scheme(.)", filename)
if m:
    print m.group(0)    # channela_scheme1
    print m.group(1)    # a
    print m.group(2)    # 1
    print m.groups()    # ('a', '1')
    print m.groupdict() # empty dict
else:
    print "no match"

#%% Extracting the channel index and the scheme index (using subexpressions with names)
# the name-match pairs are returned by groupdict() as a dictionary 
m = re.search(r"channel(?P<ch>.)_scheme(?P<sch>.)", filename)
if m:    
    print m.group(0)    # channela_scheme1
    print m.group(1)    # a
    print m.group(2)    # 1
    print m.groups()    # ('a', '1')
    print m.groupdict() # {'ch': 'a', 'sch': '1'}
else:
    print "no match"

#%% Can extract channel separately
m = re.search(r"channel(?P<ch>.)", filename)
if m:
    print m.group(0)    # channela
    print m.group(1)    # a
    print m.groups()    # ('a',)
    print m.groupdict() # {'ch': 'a'}
else:
    print "no match"
    
#%% Or extract channel separately
m = re.search(r".*scheme(?P<sch>.)", filename)
if m:
    print m.group(0)    # channela_scheme1
    print m.group(1)    # 1
    print m.groups()    # ('1',)
    print m.groupdict() # {'sch': '1'}
else:
    print "no match"        
```

match
```
#%% search vs match
# re.match() checks for a match only at the beginning of the string, 
# while re.search() checks for a match anywhere in the string 
# (this is what Perl does by default).

# re.match does not find a match
m = re.match(r"scheme(?P<sch>.)", filename)
if m:
    print m.group(0)    # channela_scheme1
    print m.group(1)    # 1
    print m.groups()    # ('1',)
    print m.groupdict() # {'sch': '1'}
else:
    print "no match"    

# but re.search does
m = re.match(r".*scheme(?P<sch>.)", filename)
if m:
    print m.group(0)    # channela_scheme1
    print m.group(1)    # 1
    print m.groups()    # ('1',)
    print m.groupdict() # {'sch': '1'}
else:
    print "no match"    
```
