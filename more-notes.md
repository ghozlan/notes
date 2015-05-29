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

