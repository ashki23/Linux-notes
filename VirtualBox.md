# VirtualBox

Download the latest version of Oracle VirtualBox from [here](https://www.virtualbox.org/). Then install the iso file of the OSs that you are looking for to install such as Ubuntu, CentOS, Fedora and etc.

It is pretty simple to create the VM. Just click on the New under Machine tab and follow the structure to the end. Note that if the iso file is larger increase the VM storage (it is 8G by default).

After creating the VM:
- Click on the MV and select Setting > Storage and add the iso from Controller IDE - Empty > Optical Drive > Choose a disk file. Then start the VM and install the ISO
- After installing OS, turn off the MV and go to the setteing and remove the added iso from Setting > Storage
- Go to Setting > System and change the Boot Order and put Hard Disk to the top of the list
- Start the VM again and from top menu select Devices > Insert Guest Additions CD Image
- Then go to the CD drive of the OS and run the application (review [here](https://askubuntu.com/questions/314685/is-there-a-way-to-make-a-fullscreen-on-virtualbox) or search how to make a fullscreen on VirtualBox)
- Reboot the VM, open the OS Setting and change the VM resulution 



