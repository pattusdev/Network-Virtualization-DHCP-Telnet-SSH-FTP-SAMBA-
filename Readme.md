# Configure Linux Server With DHCP-Telnet-SSH-FTP-SAMBA-


### Requirements:
- Windows server 2003 disc image
- REHL 6 disc image
- Microsoft Windows XP Professional SP3 disc image(my favorite)
- Virtualbox 6.1.30
- Virtualbox extension 6.1.30
- Microsoft Exchange 2003
- Microsoft Office 2007
- Faster machine is an added asset


#### NB: The sequence written here isn’t definite but it makes it 
easier to follow this way.
1. Install Red hat while it starts installation 
2. Install Windows server
3. Install Windows XP3
4. Check if red hat is done, start with the commands, when you 
reach to `cp * -v /2022` command, check on Windows machine
5. When you reach on `createrepo –v/2022/`, Install exchange on 
windows server, while you are waiting for forest preparation 
to be done, install MS Office on your XPs
### Steps of installing virtual box:
1. Install virtual box
2. After installation, click on preferences – click on extensions –
click on add icon on the right side – add the Virtualbox 
extension.
### Let’s move on with the project:
> First we install RHEL Server:
- Click on New
- Name the machine label (RHEL Server _ Your ID e.g: RHEL 
Server_23580)
- On type, choose Linux
- On version, choose Red Hat(64-bit)
- Memory size use 512 MB
- On Hard disk, choose Create a virtual hard disk now
- Hard disk file type, choose VDI(Virtual Disk Image)
- Storage on physical hard disk, choose dynamically allocated.
- File location and size, choose 20GB and leave the folder 
untouched(default)
- Click on settings icon
- General – Advanced – Shared clipboard – change disabled to 
bidirectional – drag’n’drop – change disabled into 
bidirectional( This allows you to copy paste between the 
host[physical machine] and VM)
- Storage – Controller:IDE – Empty – click on disc icon next to 
optical drive on the left part of the dialog box – choose a disk 
file(if it’s not listed automatically) – Go to where Red hat 
disc image is stored on the machine.
- Network – attached to: choose bridged adapter(This allows 
connectivity between the VM) - OK
- Start the VM
- Choose Install or upgrade
- Skip – Next – Next – Next – Basic storage devices – Next – Reinitialize all – Hostname(you can choose any name – let’s use 
SERVER) – Time zone: Africa/Kigali - Next 
- Root password: auca@2020 (Unless noted otherwise) Root is a 
Linux super-user somewhat like the administrator.
- Type of installation, choose Create custom layout
- Please select a device – click on Free under Hard drives –
create – Standard partition – Create – Mount Point, choose / -
File system type leave it untouched(ext4) – size(MB) 10000 – OK
- Click on Free again – Standard partition – Create – Leave mount 
point untouched(Blank space) – File system type, choose Swap –
Size(MB)= 2*RAM(if you assigned during installation in 
virtualbox RAM of 512 as we did, then size will be equal to (1024) – OK – Next – Format – Write changes to disk - Next–
Default installation, Choose Desktop – Next – Wait.
- Reboot – Forward – Forward – Forward – Forward – Create user, 
Username write: Pattus(you can change it to whoever you want), 
Password: auca@2020(it’s not ideal to use same passwords in 
physical world but for the sake of remembering all these 
passwords, I strongly recommend 1 password throughout this 
project: auca@2020) – Forward – Forward – OK – Finish
- Login as Other – username, write: root – password, write: 
auca@2020
- Tick Do not show me this again – close – right click (not left 
click) on two computer icon on the left top corner of the screen 
– Edit connections – choose System eth0 – Edit – Tick connect 
automatically – apply (Notice that there a loading sign where 
the computers were, I noticed that this somehow helps the 
problem of not activation of network after the ip addresses are 
given.) – Open terminal (The following are the commands, they 
are in successive order and they are bold like this, next to 
them are what they do at least those I know their role.)

### REDHAT SERVER DHCP CONFIGURATION COMMANDS

> As the domain name or window domain controller name is not yet 
revealed for our exam, I used those of the project. Domain name as
jubilee.org and windows domain controller name as server.jubilee.org.
Also the subnet I used is same as that of the project 192.168.10.0/24.
Linux terminal is case sensitive, so upper case is upper case and 
lower case is lower case.
- `setup` this helps us to access the network 
configuration tab – Network Configuration – Device configuration 
– eth0 (eth0) – Intel ... – Enter – TAB – TAB – space (to remove 
the star which allows us to use static IP) – static IP, write: 
192.168.10.2 – Net mask, write: 255.255.255.0 – Default gateway, 
write: 192.168.10.1 – Primary DNS Server, write: 8.8.8.8(Google 
DNS Server) – TAB key – TAB key – OK – TAB key – Save – TAB key 
– Save&Quit – TAB key – TAB key – Quit
- `service NetworkManager start` This starts service called 
network manager
- `service network restart` To enforce the changes we’ve made 
regarding IPs
- `mkdir /2022` We create a directory we’ll be working in – go to 
devices at the top of the red hat window – Optical drives – Red 
hat disc image
- `cd /media/RHEL(*press TAB*)/Packages` This helps us to enter that 
directory we specified, the whole command looks like this cd 
/media/RHEL_6.0\ i386\ Disc\ 1/Packages 
- `cp * -v /2022` wait...
- `rpm –ivh deltar(press TAB)` this installs that service, the 
whole command looks like this rpm –ivh deltarpm-3.5-
0.5.20090913git.el6.i686.rpm
- `rpm –ivh python-deltar(press TAB)` This is also installing 
command, whole command looks like this rpm –ivh python-deltarpm-3.5-0.5.20090913git.el6.i686.rpm 
- `rpm –ivh createrepo(press TAB)` This also installs that 
service, the whole command looks like this rpm –ivh createrepo-0.9.8-4.el6.noarch.rpm 
- `createrepo –v /2022/` This create a repository of 2680 items, 
so wait till it’s done
- `vim /etc/yum.repos.d/Pattus.repo` This opens a file to add 
information about our repository and server in general. The name 
Pattus can be changed to anything other than the directories you 
have or created, this certainly excludes 2022. 

 
 _First press **i** to be able to insert anything._
 _Write:_
 ```
 [server] press enter
 name= Linux Server
 baseurl=file:///2022
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
vim /etc/yum.repos.d/Pattus.repo
- `yum install dhcp –y` This is to install dynamic host 
configuration protocol which is responsible to 
assigning IPs automatically, yum is an acronym to say 
Yellowdog Updater, Modified (YUM) used to install RPM 
packages for Linux based computers developed by Seth 
Vidal and is written in python. You should get message 
saying complete!, If not and you get error downloading 
package, minimize the terminal and click on the 
cd(RHEL_6.0 i386 Disc 1), choose Packages, type dhcp, 
double click on it, click Continue Anyway, Install –
when done return to the terminal
- `rpm –qa dhcp` To check if dhcp is installed, you 
should get the version of it otherwise it’s not 
installed
- `cp /usr/share/doc/dhcp-4.1.1/dhcpd.conf.sample 
/etc/dhcp/dhcpd.conf` This is linux command of 
copying and pasting, the first path is the directory of 
origin and the latter is the destination. They ask you 
if you want to overwrite, type `y`
- `vim /etc/dhcp/dhcpd.conf` This is where we copied 
that file and we open it to edit it tailoring it to the 
specific needs of our network 
GO TO LINE 47(Lines are displayed on the bottom 
part of the terminal at the right side where it’s 
written 1, 1 as you move down it changes 
regarding to where you are).
    * Subnet `192.168.10.0` netmask `255.255.255.0`;
    * Range (This is the range you want this 
server to start with while giving IPs, the 
first IP address is the starting IP and the 
second one is the last IP you want to give, 
this depends on machines you have which 
will need IP since we only have 3 clients 
machine, we can give if we want a range of 
10 IPs) range `192.168.10.5` `192.168.10.20`;
(We skip the static IPs we gave earlier we 
used `192.168.10.0` as subnet IP, 
`192.168.10.1` as default gateway, 
`192.168.10.2` as Red hat IP, `192.168.10.3` as 
Windows Server)
    * Option domain-name-servers 
`server.jubilee.org`;(we type the full name 
of our domain controller, it is composed 
first by the name of server then the domain 
name, to know it you open domain controller 
server and right click my computer –
properties – computer name – and see where 
it’s written full computer name, and that’s 
should be written there.
    * Option domain-name `“jubilee.org”`;(This is 
the domain name, it’s found below the full 
computer name on domain controller server)
    * Option routers `192.168.10.1` (this is our 
default gateway)
    * Line 52 must be deleted entirely (This line 
have info about broadcast but our system 
can detect it from the subnet we provided 
so, deleting this line is the simplest way)
    * Default-lease-time and max-lease-time 
should be left as default unless otherwise 
noted. It’s also crucial to know that it’s 
in seconds.
    * Press ESC, Shift + semi colon, write, wq –
press ENTER
> it should looks like this,
```
# A slightly different configuration for an internal subnet.
subnet 192.168.10.0 netmask 255.255.255.0 {
    range 192.168.10.5 192.168.10.20;
    option domain-name-servers dcserver.chogm.rw;
    option domain-name "chogm.rw";
    option routers 192.168.10.1;
    default-lease-time 600;
    max-lease-time 7200;
}
```
![Linux Server DHCP Conf.](https://github.com/pattusdev/Network-Virtualisation-DHCP-Telnet-SSH-FTP-SAMBA-/blob/main/images/Capture.JPG)

- `service dhcpd start` This starts our dynamic host 
configuration protocol service and the output must be 
[OK] if it’s [FAILED] means you have to troubleshoot. 
The d ending dhcpd means daemon, it’s like the 
controlling service of DHCP and the beginning should be 
dhcpd –t command it allows you to know where the 
mistake is, good luck!
- `chkconfig dhcpd on` This ensures that every time RHEL 
server is powered on, service dhcpd is started 
automatically, ain’t a fan of powering off, I’m more of 
save machine state guy.

### REDHAT SERVER TELNET CONFIGURATION COMMANDS

Telnet allows us to access the terminal/prompt or shell whatever 
name you use of a telneted machine. If you telnet 192.168.10.2 from 
windows XP, that means that you will access the shell/terminal of 
redhat server in this particular network we are building. As always 
commands are written in `bold like this`. Let’s go.

- `rpm –qa telnet` This is to check if telnet is installed, if it 
is you get its version, if not you install it using this command 
yum install telnet –y you get complete! Message, if it refuse, 
use the manual way we did earlier.
- `rpm –qa telnet-server` This is to check if telnet-server is 
installed, if it is you get its version, if not you install it 
using this command yum install telnet-server –y you get complete! 
Message, if it refuse, use the manual way we did earlier.
- `rpm –qa xinetd ` This is to check if xinetd is installed, if 
it is you get its version, if not you install it using this 
command yum install xinetd –y you get complete! Message, if it 
refuse, use the manual way we did earlier.
- `cd /2022` This changes directory to 2022 
- `vim /etc/xinetd.d/telnet` This is to open configuration of 
telnet 

 _First press **i** to be able to insert anything._
 _Write:_
```
disable = no
```
 _then press ESC key_
 _hold shift+semi colon_
 _write:_ 
 ```
 wq
 ```
_press ENTER key_
- `service xinetd start` This starts our telnet service you must 
get [OK] if not troubleshoot.
- `setup` This allows us to access firewall configuration dialog 
box to turn it off. Choose Firewall configuration – space (to remove the star which enables firewall) – TAB key – OK – Yes -
TAB key – Quit
- `useradd Pattus`This is the command to create users which will 
use our telnet service, the name Pattus can be replaced by any 
name you want or as it is specified per instruction 
- `passwd Pattus` This prompts to password setting, it’s not by 
any means the password 
- `auca@2020` This is the password we’ve been using it is written 
as the system prompts for password, as you type nothing happens, 
this is security measure common in Linux OS.

### REDHAT SERVER SECURE SHELL (SSH) CONFIGURATION
Telnet although that useful have one simple problem, it transmits 
commands as text which aren’t encrypted, so if anyone is using 
softwares like wireshark can sniff on your network and steal 
passwords and info. (Cybersecurity, my dream field). SSH, solves 
this problem as it transmits encrypted commands and passwords hence 
more secure but functionality is same as telnet. SSH is built-in, we 
don’t have to anything but check that it’s working. As of now, I 
won’t explain the commands unless it’s new one, you’ve become 
familiar. Let’s go!
- `rpm –qa openssh` Whatever is not installed you install it
- `rpm –qa xinetd`
- `rpm -qa rpcbind` if it’s not installed, you install this by yum 
install portmap –y 
- `service sshd status` To check if they are working, you get 
output “... is running”. If it is stopped type service sshd 
start 
- `service xinetd status`
- `service rpcbind status`
- `chkconfig sshd on`
- `chkconfig rpcbind on`

### REDHAT SERVER SAMBA CONFIGURATION
File and resources sharing irrespective of OS is made possible by 
samba services. Here we are going to share a directory named share
across our network seamlessly even though we are different OS. 
Let’s go!!
- `rpm –qa samba`
- `rpm –qa samba-common`
- `rpm –qa samba-winbind`
- `rpm –qa samba-winbind-clients`
- `mkdir /share/`
- `cd /`
- `ls`
- `ls –ldZ /share/`
- `chmod 777 /share/` 
- `chcon –t samba_share_t share`
- `ls –ldZ /share/` You should get output like this “ drwxrwxrwx. 
root root unconfined_u:object_r:samba_share_t:s0 /share/ ”
- `smbpasswd –a Pattus` This is to add our user we created 
earlier in telnet on users allowed to user samba, if you want 
you can create other users right now using the command useradd

- `auca@2020` if it prompts you to create password, you should get 
message saying Added user Pattus 
- `Pdbedit –L`  To check a list of samba users 
- `vim /etc/samba/smb.conf`  to open samba configuration file
_press shift+g to go to the bottom of the 
file_
_press **i** to insert anything_
_remove all the semi colon on the last 7 
lines_
_the file looks like this:_
```
; [public]
; comment =Public stuff
; path =home/samba
; public =yes
; writable =yes
; printable =no
; write list =+staff
```
_It should be edited to look like this and 
the lines which aren’t there must be added:_
```
[share]
comment =domain stuff
path =/share
public =no
writable =yes
printable =no
write list =+staff
valid users =Pattus
hosts allow =192.168.10.
```
 _then press ESC key_
 _hold shift+semi colon_
 _write:_ 
 ```
 wq
 ```
_press ENTER key_

- `testparm` This is to see if our configured file info is 
recognized by the system you should first see message saying 
“Loaded services file OK” press ENTER key to see all 
- `service smb start`
- `service nmb start`
- `chkconfig smb on`
- `chkconfig nmb start`

### REDHAT SERVER FILE TRANSFER PROTOL (FTP) CONFIGURATION
As its name explains it transfers files throughout the network. 
It commonly uses port 21 but it may vary. Let’s go!
- `mount /dev/cdrom /mnt` This is a command to mount the Red Hat CD 
you first insert it via devices – optical drives – you know the 
drill... . The output should be like this “mount: block 
device...” 
- `df –h`
- `yum install vsftpd –y` to install very secure file transfer 
protocol daemon if it’s not installed 
- `vim /etc/vsftpd/vsftpd.conf`to edit vsftpd configuration file 
_press Shift key + g to go to the end of 
file_
_press i to insert anything_
_write:_
``` 
userlist_deny=NO
``` 
_(to make a list of 
authorized users)_
 _then press ESC key_
 _hold shift+semi colon_
 _write:_ 
 ```
 wq
 ```
_press ENTER key_

- `vim /etc/vsftpd/user_list` To add authorized users on ftp user 
list – press i to insert – write the names of users authorized to 
use ftp, in this scenario I created only 1 user, under nobody 
write Pattus – press ESC key – press SHIFT key + semi colon –
write, wq – Press ENTER key. 
- `getsebool –a | grep ftp` To check if SElinux is configured or 
not to allow upload/download in user’s home directory 
- `setsebool ftp_home_dir=on` If SELinux is configured to allow 
upload/download use this command to allow it. 
- `service vsftpd start`

<br />
<br />
<br />

### [USEFUL-LINKS!]

> Configure Linux Server With [DHCP-Telnet-SSH-FTP-SAMBA](https://github.com/pattusdev/Network-Virtualization-DHCP-Telnet-SSH-FTP-SAMBA-/blob/main/Readme.md).


> A Quick-Jump to Installing [Windows Server 2003](https://github.com/pattusdev/Network-Virtualization-DHCP-Telnet-SSH-FTP-SAMBA-/blob/main/Windows%20Server%202003.md).


> Installing Clients Machines [REDHAT CLIENT AND TWO XP CLIENT MACHINES Also Testing!!](https://github.com/pattusdev/Network-Virtualization-DHCP-Telnet-SSH-FTP-SAMBA-/blob/main/RedHat%2C%20XP%20Client%20Hosts.md).


> Check This [Linux Cheat Sheet](https://github.com/pattusdev/Network-Virtualization-DHCP-Telnet-SSH-FTP-SAMBA-/blob/main/Linux-cheat-code.md).
