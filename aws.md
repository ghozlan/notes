# Amazon Web Services

## Free Tier

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

### Elastic MapReduce (EMR)
* None. See [pricing](http://aws.amazon.com/elasticmapreduce/pricing/).

## Creating an EC2 Instance
Compute> EC2>
* Launch Instance
* Select: Ubuntu Server 14.04 LTS (HVM), SSD Volume Type, 64-bit [free tier]
* Select: t2.micro: 1 vCPU, 1 GiB memory, EBS only storage [free tier]
* Select Security Group?
* Select a Key Pair

## Connecting to an Instance
Compute> EC2> Instances> Instances
* Add a name tag (optional).
* Note down the Public DNS or Public IP (will need one of them for connecting to terminal)
  * Default user: ubuntu
* Use PuTTY
  * Connect to: ubunu@(Public DNS) or ubuntu@(Public IP)
  * Note: To paste (from clipboard), just right-click in the window area.
* Or use ssh: `ssh -i <key>.pem ubuntu@host` (remember to set the permissions of the key: `chmod 600 <key>.pem`)
* Use *screen* command (neat tool for handling screens/windows in command line)
  * Ctrl+a ?: help
  * Ctrl+a c: create new screen
  * Ctrl+a A: set title for screen
  * Ctrl+a ": select screen from list  
  * Ctrl+a d: detatch
  * Splitting into regions:
    * Ctrl+a S (Shift+s): split vertically
    * Ctrl+a | : split horizontally
    * Ctrl+a tab : switch focus between regions
    * Ctrl+a X (Shift+x): remove/kill the current region (the region in focus)
  * screen -r: resume session

## Transferring files 
### FileZilla
* Edit> Settings> Connection> SFTP> 
  * Add keyfile
* File> Site Manager> New Site
  * Host: (Public IP) or (Public DNS)
  * Port: leave blank (default will be used)
  * Protocol: SFTP
  * Logon Type: Normal
  * User: ubuntu
  * Password: leave blank (we are using a key instead)
  * Connect

### secure copy: scp
```
scp -i <key>.pem <filename> user@hotname:/home/user/
```
Remember to set the permissions of the key `chmod 600 <key>.pem`

## Adding Elastic Block Store (EBS) Volume
Compute> EC2> Elastic Block Store> Volume
* Create volume.
  * Watch out for the size! There is a limit for the free tier. 
  * Watch out for the availability zone!
* Add a name tag (optional).
* Select the volume, then from Actions, select Attach Volume (suppose it is attached as /dev/sdf).
* Connect to the instance to which the volume is attached
* Format the volume (once)

  ```
  sudo mkfs -t ext4 /dev/xvdf
  ```

* To mount the device as /mnt/mydata, run 

  ```
  sudo mkdir /mnt/my-data
  sudo mount /dev/xvdf /mnt/mydata
  ```

[Reference](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-add-volume-to-instance.html)

## Installing packages:
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

### Matplotlib error
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
To fix this error, insert the following berfore any other pylab/matplotlib import
```
import matplotlib
matplotlib.use('Agg') # force matplotlib to not use any Xwindows backend.
```
[Reference: stackflow](http://stackoverflow.com/questions/2801882/generating-a-png-with-matplotlib-when-display-is-undefined)
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

## Installing MySQL Server
To install, run
```
sudo apt-get install mysql-server
```
You will be prompted to choose the root password.
To start using mysql server, run
```
mysql --user=<user> --pass=<password>
```

## Installiing MySQL Connector
Using pip

```
sudo pip install --allow-external mysql-connector-python mysql-connector-python 
```
[Reference](https://geert.vanderkelen.org/installing-coy-using-pip/)
 
## Adding Virtual Memory

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


## Useful Linux Commands

Disk/storage
```
df -h
sudo fdisk -l | grep Disk
lsblk
cat /etc/fstab
```

Skip the first line of a file
```
tail <filename> -n+2
```
Get unique entries in a field (in csv, tsv,...etc) and their count
```
cut <filename> -f<field-number> -d<delimiter> | sort | uniq -c | sort -r
```
The previous two lines can be combined (piped)
```
tail <filename> -n+2 | cut -f<field-number> -d<delimiter> | sort | uniq -c | sort -r
```


## Useful Linux Tools
* diff
  * diff -y (side-by-side)
* colordiff
* htop
* nano
* netstat
  ```
  netstat -lan
  ```
* tcpdump
  * Capture http traffic and write `-w` to file `capture.cap`
   ```
   sudo tcpdump port http -w capture.cap
   ```
  * Display the packets of a file called `capture.cap`:
   ```
   tcpdump -r capture.cap
   ```
  * `-v`,`-vv`,`--v`: vebosity level.
  * `src port` and `dst port` to specify a source or destination port respectively.
  * `-n`: do not resolve names.
  * `-i <interface>`: specify the network interface. `-i any` captures traffic on any interface.
  
 [Ref](http://www.rationallyparanoid.com/articles/tcpdump.html)
* nmap
* lynx

## nano
* For help/guide, press Ctrl+G
* To cut/copy and paste multiple lines:
  1. At the first line, press Ctrl+^ (Ctrl+Shift+6) to start marking the lines.
  2. Move the cursor using arrow keys to the last line (and see the lines being highlighted).
  3. Press Ctrl+K to cut (kut) or Alt+M (or is it Alt+6?) to copy.
  4. Press Ctrl+U to paste (uncut).
* Hint: Pressing Ctlr+U multiple times will paste (uncut) the buffer multiple times. This can be used to copy/paste.
* Indent/Unindent: press Alt+} (Alt+Shift+]) to indent and press Alt+{ (Alt+Shift+[) to unindent. 

