# Configure Linux Server With DHCP-Telnet-SSH-FTP-SAMBA-


Requirements:
- Windows server 2003 disc image
- REHL 6 disc image
- Microsoft Windows XP Professional SP3 disc image(my favorite)
- Virtualbox 6.1.30
- Virtualbox extension 6.1.30
- Microsoft Exchange 2003
- Microsoft Office 2007
- Faster machine is an added asset
NB: The sequence written here isn’t definite but it makes it 
easier to follow this way.
1. Install Red hat while it starts installation 
2. Install Windows server
3. Install Windows XP3
4. Check if red hat is done, start with the commands, when you 
reach to cp * -v /2022 command, check on Windows machine
5. When you reach on createrepo –v/2022/, Install exchange on 
windows server, while you are waiting for forest preparation 
to be done, install MS Office on your XPs
Steps of installing virtual box:
1. Install virtual box
2. After installation, click on preferences – click on extensions –
click on add icon on the right side – add the Virtualbox 
extension.
Let’s move on with the project:
 First we install RHEL Server:
 Click on New
 Name the machine label (RHEL Server _ Your ID e.g: RHEL 
Server_23580)
 On type, choose Linux
 On version, choose Red Hat(64-bit)
 Memory size use 512 MB
 On Hard disk, choose Create a virtual hard disk now
 Hard disk file type, choose VDI(Virtual Disk Image)
 Storage on physical hard disk, choose dynamically allocated.
 File location and size, choose 20GB and leave the folder 
untouched(default)
 Click on settings icon
 General – Advanced – Shared clipboard – change disabled to 
bidirectional – drag’n’drop – change disabled into 
bidirectional( This allows you to copy paste between the 
host[physical machine] and VM)
 Storage – Controller:IDE – Empty – click on disc icon next to 
optical drive on the left part of the dialog box – choose a disk 
file(if it’s not listed automatically) – Go to where Red hat 
disc image is stored on the machine.
 Network – attached to: choose bridged adapter(This allows 
connectivity between the VM) - OK
 Start the VM
 Choose Install or upgrade
 Skip – Next – Next – Next – Basic storage devices – Next – Reinitialize all – Hostname(you can choose any name – let’s use 
SERVER) – Time zone: Africa/Kigali - Next 
 Root password: AUCA@2020 (Unless noted otherwise) Root is a 
Linux super-user somewhat like the administrator.
 Type of installation, choose Create custom layout
 Please select a device – click on Free under Hard drives –
create – Standard partition – Create – Mount Point, choose / -
File system type leave it untouched(ext4) – size(MB) 10000 – OK
 Click on Free again – Standard partition – Create – Leave mount 
point untouched(Blank space) – File system type, choose Swap –
Size(MB)= 2*RAM(if you assigned during installation in 
virtualbox RAM of 512 as we did, then size will be equal to 
1024) – OK – Next – Format – Write changes to disk - Next–
Default installation, Choose Desktop – Next – Wait.
 Reboot – Forward – Forward – Forward – Forward – Create user, 
Username write: Yves(you can change it to whoever you want), 
Password: AUCA@2020(it’s not ideal to use same passwords in 
physical world but for the sake of remembering all these 
passwords, I strongly recommend 1 password throughout this 
project: AUCA@2020) – Forward – Forward – OK – Finish
 Login as Other – username, write: root – password, write: 
AUCA@2020
 Tick Do not show me this again – close – right click (not left 
click) on two computer icon on the left top corner of the screen 
– Edit connections – choose System eth0 – Edit – Tick connect 
automatically – apply (Notice that there a loading sign where 
the computers were, I noticed that this somehow helps the 
problem of not activation of network after the ip addresses are 
given.) – Open terminal (The following are the commands, they 
are in successive order and they are bold like this, next to 
them are what they do at least those I know their role.)
