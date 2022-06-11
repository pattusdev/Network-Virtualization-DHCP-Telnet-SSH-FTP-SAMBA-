- `mkdir /YOURID` We create a directory we’ll be working in – go to 
devices at the top of the red hat window – Optical drives – Red 
hat disc image
```
mkdir /YOUR_ID
```
- `cd /media/RHEL(*press TAB*)/Packages` This helps us to enter that 
directory we specified, the whole command looks like this cd 
/media/RHEL_6.0\ i386\ Disc\ 1/Packages 
- `cp * -v /YOURID` wait...
- `rpm –ivh deltar(press TAB)` this installs that service, the 
whole command looks like this rpm –ivh deltarpm-3.5-
0.5.20090913git.el6.i686.rpm
- `rpm –ivh python-deltar(press TAB)` This is also installing 
command, whole command looks like this rpm –ivh python-deltarpm-3.5-0.5.20090913git.el6.i686.rpm 
- `rpm –ivh createrepo(press TAB)` This also installs that 
service, the whole command looks like this rpm –ivh createrepo-0.9.8-4.el6.noarch.rpm 
- `createrepo –v /YOURID/` This create a repository of 2679 items, 
so wait till it’s done
- `vim /etc/yum.repos.d/THECHOOSENNAME.repo` This opens a file to add 
information about our repository and server in general. The name 
Pattus can be changed to anything other than the directories you 
have or created, this certainly excludes 2022. 

 
 _First press **i** to be able to insert anything._
 _Write:_
 ```
 [server] press enter
 name= Linux Server
 baseurl=file:///YOURID
 enabled=1
 gpgcheck=0
 ```
 _then press ESC key_
 _hold shift+semi colon_
 _write:_ 
 ```
 wq
 ```
 _( w means save and q means quit)_
 _press ENTER key_
 
 - `yum repolist` This loads the installed repository, if 
the number is equal to 2679, good, if not don’t worry 
continue with the next command
- `cd /etc/yum.repos.d/` we are changing directory to 
the specified path
- `ls` This list everything inside a directory, we want 
to see if this folder have our Pattus.repo only, if not, 
it might have also packagekit-media.repo. This one must 
be removed using this command rm –f packagekit-media.repo now do ls again, you only have Pattus.repo now 
do yum repolist now you should have 2679. If not you 
should do further troubleshooting mainly in the file we 
edited and check if everything is written as it should, 
you can access the file by typing this command:
vim /etc/yum.repos.d/THECHOOSENNAME.repo
<br />
<br />
<br />

### [USEFUL-LINKS!]

> Configure Linux Server With [DHCP-Telnet-SSH-FTP-SAMBA](https://github.com/pattusdev/Network-Virtualization-DHCP-Telnet-SSH-FTP-SAMBA-/blob/main/Readme.md).


> A Quick-Jump to Installing [Windows Server 2003](https://github.com/pattusdev/Network-Virtualization-DHCP-Telnet-SSH-FTP-SAMBA-/blob/main/Windows%20Server%202003.md).


> Installing Clients Machines [REDHAT CLIENT AND TWO XP CLIENT MACHINES Also Testing!!](https://github.com/pattusdev/Network-Virtualization-DHCP-Telnet-SSH-FTP-SAMBA-/blob/main/RedHat%2C%20XP%20Client%20Hosts.md).


> Check This [Linux Cheat Sheet](https://github.com/pattusdev/Network-Virtualization-DHCP-Telnet-SSH-FTP-SAMBA-/blob/main/Linux-cheat-code.md).

