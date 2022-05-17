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
5. When you reach on createrepo –v/2022/, Install exchange on 
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
- Root password: AUCA@2020 (Unless noted otherwise) Root is a 
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
Password: AUCA@2020(it’s not ideal to use same passwords in 
physical world but for the sake of remembering all these 
passwords, I strongly recommend 1 password throughout this 
project: AUCA@2020) – Forward – Forward – OK – Finish
- Login as Other – username, write: root – password, write: 
AUCA@2020
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
command, whole command looks like this rpm –ivh python-deltarpm-3.5-0.5.20090913git.el6.i686.rpm */
- `rpm –ivh createrepo(press TAB)` This also installs that 
service, the whole command looks like this rpm –ivh createrepo-0.9.8-4.el6.noarch.rpm */
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
![This is an image](https://myoctocat.com/assets/images/base-octocat.svg)
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
save machine state guy
