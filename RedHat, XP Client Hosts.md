### INSTALLING CLIENTS MACHINES: REDHAT CLIENT AND TWO XP CLIENT MACHINES Also Testing!!
- I know you like easy way but ain’t a fan of cloning so, I
strongly recommend you install red hat client as we installed red 
hat server the only difference is on hostname we use client 
instead of server as earlier. XP machines installation is similar 
to that of windows server 2003 the exception is on the name of 
computer. We only need to use them to see if all services we 
configured in servers can be accessed by clients.
>After installation of red hat
Let’s check if we can use DHCP, Telnet, SSH, Samba, FTP services
- Login as Other – username, write: root – password, write: 
auca@2020
- Tick Do not show me this again – close – right click (not left 
click) on two computer icon on the left top corner of the screen 
– Edit connections – choose System eth0 – Edit – Tick connect 
automatically – apply (Notice that there a loading sign where 
the computers were, I noticed that this somehow helps the 
problem of not activation of network after the ip addresses are 
given.) – Open terminal (The following are the commands, they 
are in successive order and they are `bold like this`, next to 
them are what they do at least those I know their role.)
o DHCP
If we can get automatic IP that means our dhcp service is 
working so let’s see.
Open terminal – type the following commands:
- `ifconfig eth0` To see the IP we have, if it’s some 
random things, we need to set up our IPs 
- `setup` go to network configuration like earlier – the 
star on Use DHCP should be left untouched – on primary 
DNS server type IP address of windows server – save
and exit as earlier 
- `ifconfig eth0` To see the IP we have, it should be in 
the range we configured in red hat server 
o TELNET
- `rpm –qa telnet`  if it’s not there, you install it
manually as earlier 
- `telnet 192.168.10.2`  Login: Kevin , password: 
auca@2020, notice how the terminal changes to 
[Kevin@server /], you can change to root by typing 
this command `su root` it prompts root password 
auca@2020, now terminal looks like this 
[root@server /]# , now we know telnet works 
o SSH
- `yum install ssh -y`
- `ssh 192.168.10.2` It asks you if you want to connect 
to the mentioned device and add it on , type yes it 
prompts you to root password, if you enter it ,done it 
works also 
o FTP
- `yum install ftp -y`
- `ftp 192.168.10.2` insert the name of the authorized
user and his/her password, notice how the terminal 
changes to ftp> , now you can use linux commands to 
get files you need 
o SAMBA
- `smbclient –L 192.168.10.2 –U Kevin` To list out 
the samba share on client machine, you will see our 
folder we shared 
- `smbclient //192.168.10.2/share –U Kevin` To access 
the samba share 
After installation of XP :
- Welcome to Microsoft windows – next – Not right now – next –
choose Local Area Network – Next – setting up a high speed 
connection – skip – Ready to register with Microsoft, tick no,
not at this time – Next – Your name: type Yves – Next - Finish
Giving windows xp a static IP (Before joining domain)
- Windows Key + R (or Click start – Run) – write: ncpa.cpl(to 
access network connections) – click change windows firewall 
settings – off – OK - Right click on Local Area connection –
properties – Internet Protocol(TCP/IP) – use the following IP –
IP is 192.168.10.4 – subnet mask is 255.255.255.0 – default 
gateway is 192.168.10.1 – primary DNS server is 192.168.10.3 –
OK – OK.
Inserting Guest Additions CD
- Devices – optical drives – remove disc from virtual drive –
devices – insert guest additions cd image – Next – Next –
Install – Finish – after reboot
Joining the jubilee domain:
- Right click on my computer – properties – Computer name tab –
change (last line) – tick member of Domain – type jubilee –
username: type Administrator – password: auca@2020 – welcome to 
Jubilee domain – OK – Restart the PC – after reboot log in as 
administrator
Installing MS Office 2007:
- Devices – remove disc from virtual drive – devices – optical 
drive – choose disk file – go to where you saved MS Office disc 
image and product key – click on CD – it prompts you to enter 
product key it might be CM9R7-9X4DV-F43J4-JVC67-GYDQ8 if we have 
same software.
Installing filezilla:
- To use ftp we need to use filezilla,(I assume the software is 
saved on physical machine, you share it as we did earlier then 
copy it on your xp and install it as any other software)
Checking if DHCP works:
- Use ncpa.cpl to access the LAN – right click on it – properties 
– Internet Protocol TCP/IP – choose acquiring IP automatically, 
notice how the fields for IP turns blank – OK – OK – notice how 
under LAN is written Acquiring IP address – wait till it changes 
to connected – open command prompt type ipconfig /all and notice 
how on dhcp enabled is yes
After this log out and log in as registered user of the active 
directory.
Checking if Telnet works:
- Open command prompt by using windows + R – type: cmd – in cmd 
write telnet 192.168.10.2, Notice how the terminal changes to 
title saying telnet, it will prompt you to login: Kevin, 
password:auca@2020 ,if it’s successful the command line changes 
and you can do everything as if you are using red hat server
Checking if SSH works:
- Windows xp do not use ssh by default, so we need a software 
called putty, since we deployed it, if it’s not visible on the 
desktop – click start – search – all files and folders – type 
putty – drag a shortcut to the screen – open it – type 
192.168.10.2 – then connect – it should now be familiar as to 
what you did in red hat client
Checking if FTP works:
- We installed filezilla as administrator earlier, if it’s not on 
desktop , search it and drag the shortcut on screen – host: type 
192.168.10.2 password: type auca@2020 username: type: Kevin
port: type 21 – then quick connect – you will now be able to see 
two parts in filezilla, the left for your pc and right for the 
remote device. You can do whatever you want with the files
Checking if Samba works:
- Right click my computer – map network drive – drive M – path:
type: 
```
\\192.168.10.2\share
```
_finish - username: Kevin ,
password: auca@2020_
– you will open drive M – notice that if you 
open my computer you will have two network drives celebrations
and share

<br />
<br />
<br />

### [USEFUL-LINKS!]

> Configure Linux Server With [DHCP-Telnet-SSH-FTP-SAMBA](https://github.com/pattusdev/Network-Virtualization-DHCP-Telnet-SSH-FTP-SAMBA-/blob/main/Readme.md).


> A Quick-Jump to Installing [Windows Server 2003](https://github.com/pattusdev/Network-Virtualization-DHCP-Telnet-SSH-FTP-SAMBA-/blob/main/Windows%20Server%202003.md).


> Installing Clients Machines [REDHAT CLIENT AND TWO XP CLIENT MACHINES Also Testing!!](https://github.com/pattusdev/Network-Virtualization-DHCP-Telnet-SSH-FTP-SAMBA-/blob/main/RedHat%2C%20XP%20Client%20Hosts.md).


> Check This [Linux Cheat Sheet](https://github.com/pattusdev/Network-Virtualization-DHCP-Telnet-SSH-FTP-SAMBA-/blob/main/Linux-cheat-code.md).
