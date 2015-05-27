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

