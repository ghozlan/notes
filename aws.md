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
* Using PuTTY, connect to: ubunu@(Public DNS) or ubuntu@(Public IP)
* Use *screen* command (neat tool for handling screens/windows in command line)
  * Ctrl+a ?: help
  * Ctrl+a c: create new screen
  * Ctrl+a A: set title for screen
  * Ctrl+a ": select screen from list  
  * Ctrl+a d: detatch
  * screen -r: resume session
  
Installing packages:
* virtualenv?
* pip:
 * Type: pip. 

  > The program 'pip' is currently not installed. You can install it by typing:
  > sudo apt-get install python-pip

 * May need to run: 'sudo apt-get update' before 'sudo apt-get install python-pip'

* easy_install:
 * Type: easy_install.  

  > The program 'easy_install' is currently not installed. You can install it by typing:
  > sudo apt-get install python-setuptools

* IPython:
 * Type: sudo easy_install ipython

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

https://imiloainf.wordpress.com/2011/12/03/build-a-ubuntu-amazon-ec2-instance/
