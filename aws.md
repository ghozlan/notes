Amazon Web Services

Compute> EC2>
* Launch Instance
* Select: Ubuntu Server 14.04 LTS (HVM), SSD Volume Type, 64-bit [free tier]
* Select: t2.micro: 1 vCPU, 1 GiB memory, EBS only storage [free tier]
* Select Security Group?
* Select a Key Pair

Compute> EC2> Instances> Instances
* Add a name tag (optional).
* Note down the Public DNS or Public IP (will need one of them for connecting to terminal)
  * Default user: ubuntu
* Use PuTTY
  * Connect to: ubunu@(Public DNS) or ubuntu@(Public IP)
  * Note: To paste (from clipboard), just right-click in the window area.
* Use *screen* command (neat tool for handling screens/windows in command line)
  * Ctrl+a ?: help
  * Ctrl+a c: create new screen
  * Ctrl+a A: set title for screen
  * Ctrl+a ": select screen from list  
  * Ctrl+a d: detatch
  * screen -r: resume session
  
Installing packages:
* Update first
```
sudo apt-get update
```

* Python Package Management Tool: pip or easy_install
  1. pip 

     ```
     sudo apt-get install python-pip
     ```

    To obtain a list of python packages installed
    ``` 
    pip list 
    ```

  2. easy_install:

     If you type 
     ```
     easy_install
     ```
     this message will point you to which linux pacakge name to use
     ```
     The program 'easy_install' is currently not installed. You can install it by typing:
     sudo apt-get install python-setuptools
     ```

* virtualenv
```
sudo pip install virtualenv
```
or
```
sudo easy_install virtualenv
```

* IPython:
```
sudo pip install ipython
```
or
```
sudo easy_install ipython
```

* NumPy

 1. Try
    * sudo easy_install numpy [error]
 2. Try
    * sudo pip install numpy [error]
 3. Try
    * sudo apt-get install python-dev
    * Then: sudo easy_install numpy [works, but some warnings]

* SciPy
 1. Try
    * sudo easy_install scipy [error]
 2. Try
    * sudo apt-get install python-dev
    * Then type: sudo easy_install scipy [error, still]
    * Or type: sudo pip install scipy [error, still]
 3. Try
    * sudo apt-get install python-scipy [works]

* Matplotlib
 1. Try
    * sudo apt-get install matplotlib [error]
 2. Try
    * sudo pip install matplotlib [does not give error, but does not work]


### Ubunutu Package Manager [without virtualenv]
Run (in order):
```
sudo apt-get update
sudo apt-get -y install python-pip
sudo pip install ipython
sudo apt-get -y install python-numpy
sudo apt-get -y install python-scipy
sudo apt-get -y install python-matplotlib
```
The `-y` option of `apt-get` to assume *yes* as a default answer.

You can also install pandas and other packages, see [this](http://www.scipy.org/install.html#ubuntu-debian).

[Reference](https://imiloainf.wordpress.com/2011/12/03/build-a-ubuntu-amazon-ec2-instance/)

### Ubunutu Package Manager [with virtualenv]
Run (in order):
```
sudo apt-get update
sudo apt-get -y install python-pip
sudo pip install virtualenv
mkdir virtenv
virtualenv virtenv/scienv
source virtenv/scienv/bin/activate
sudo pip install ipython
sudo apt-get -y install python-numpy
sudo apt-get -y install python-scipy
sudo apt-get -y install python-matplotlib
```
The `-y` option of `apt-get` to assume *yes* as a default answer.

### Plotting in command line [error]
```
    fig = figure()
  File "/usr/lib/pymodules/python2.7/matplotlib/pyplot.py", line 423, in figure
    **kwargs)
  File "/usr/lib/pymodules/python2.7/matplotlib/backends/backend_tkagg.py", line 79, in new_figure_manager
    return new_figure_manager_given_figure(num, figure)
  File "/usr/lib/pymodules/python2.7/matplotlib/backends/backend_tkagg.py", line 87, in new_figure_manager_given_figure
    window = Tk.Tk()
  File "/usr/lib/python2.7/lib-tk/Tkinter.py", line 1767, in __init__
    self.tk = _tkinter.create(screenName, baseName, className, interactive, wantobjects, useTk, sync, use)
_tkinter.TclError: no display name and no $DISPLAY environment variable
```

### PIP Python Package Manager [no virtualenv]

Seems difficult. 

For NumPy,
```
sudo pip install numpy
```
works
but for SciPy,
```
sudo pip install scipy
```
gives error.
Probably need to install LAPCK/BLAS, which seems a bit tedious, see [this](http://www.scipy.org/scipylib/building/linux.html).


### Virtual Environment *virtualenv*

Create a directory to contain the virtual environments you will create
```
mkdir virtenv
```

To create a virtual environment, use
```
virtualenv virtenv/env1
```
or  use the ```--no-site-packages``` option:
```
virtualenv virtenv/env2 --no-site-packages
```

To activate an environment
```
user@host:~$ source virtenv/env1/bin/activate
```

To deactivate current environment

```
(env1)user@host:~$ deactivate
```

[Reference](http://simononsoftware.com/virtualenv-tutorial/)

### Adding Virtual Memory

1. Create a EBS-volume with for example 1 GB (if you want to add 1 GB virtual memory).

2. After the EBS-volume is created, attach it to the EC 2 micro instance (remember which device it is attached to (for example /dev/sdf)

3. Logged into your micro-instance, attach the new drive by doing (assuming the volume was mounted as /dev/sdf and you run Ubuntu 12.04 or later):

 ```
 mkswap -f /dev/xvdf
 swapon /dev/xvdf
 ```
 The virtual memory should now be attached. You may verify it by issuing the command:
 
 ```
 free -m
 ```

4. Attach the swap-area permanently so it survives reboots.
Edit your /etc/fstab file and add the line:

 ```
 /dev/xvdf       swap    swap    defaults        0       0
 ```

[Reference](https://damvin.com/index.php/2013/03/14/adding-virtual-memory-to-aws-ec2-micro-instances-and-other-smart-tips/)


## Hello, AWS

### Elastic Compute Cloud (EC2)
* 750 hours of 
 * Amazon EC2 Linux on t2.micro instance (1 GiB of memory and 32-bit and 64-bit platform support) 
 * Amazon EC2 Microsoft Windows Server on t2.micro instance (1 GiB of memory and 32-bit and 64-bit platform support)
 * Also RHEL, or SLES on t2.micro.
 * 750 hours is enough to run (one instance) continuously each month.
 * Can run one instance at a time or multiple instances simultaneously.
* 30 GB of Amazon Elastic Block Storage in any combination of General Purpose (SSD) or Magnetic, plus 2 million I/Os (with EBS Magnetic) and 1 GB of snapshot storage.

[Reference](http://aws.amazon.com/free/)

### Simple Storage Service (S3)
* 5 GB of Amazon S3 standard storage, 20,000 Get Requests, and 2,000 Put Requests

## Useful Linux Commands
```
df -h

sudo fdisk -l | grep Disk
lsblk

sudo mkfs -t ext4 /dev/xvdf (run once to format)
sudo mount /dev/xvdf /mnt/my-data

cat /etc/fstab

sudo mkswap -f /dev/xvdf 
sudo swapon /dev/xvdf
```

## Useful Linux Tools
* diff
  * diff -y (side-by-side)
* colordiff
* htop
* nano

## nano
* For help/guide, press Ctrl+G
* To cut/copy and paste multiple lines:
  1. At the first line, press Ctrl+^ (Ctrl+Shift+6) to start marking the lines.
  2. Move the cursor using arrow keys to the last line (and see the lines being highlighted).
  3. Press Ctrl+K to cut (kut) or Alt+M to copy.
  4. Press Ctrl+U to paste (uncut).
* Indent/Unindent: press Alt+} (Alt+Shift+]) to indent and press Alt+{ (Alt+Shift+[) to unindent. 

