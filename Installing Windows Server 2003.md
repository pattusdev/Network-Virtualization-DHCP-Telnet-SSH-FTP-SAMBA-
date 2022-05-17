### INSTALLING WINDOWS SERVER 2003
- Click on New
- Name the machine label (Windows Server)
- On type, choose Microsoft Windows
- On version, choose Windows 2003(64-bit)
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
file(if it’s not listed automatically) – Go to where Windows 
Server 2003 disc image is stored on the machine.
- Network – attached to: choose bridged adapter(This allows 
connectivity between the VM) - OK
- Start the VM
- Enter – F8(if it doesn’t work press fn+F8)
- Unpartitioned space – Enter – Format the partition using NTFS 
file system (quick) – Wait – Regional and Language options , 
choose Next
- Personalize your software: Name, write server – Organization, 
write, chogm – Next
- Enter the product key(If you have same software as me, it would 
be: DRKBX-H47BC-GRJX6-TBHFT-Y3WYB – Next – Next
- Computer name and admin password: Computer name, write: server –
password, write: auca@2020 – Next
- Date and time settings, Time zone, choose [GMT+02:00] Cairo –
Next – Network Settings, choose Typical settings – Next –
Workgroup or Computer Domain, Next - Next
### USING MICROSOFT WINDOWS SERVER 2003

- Right control + Delete (to remove the computer locked 
notification, right control is your host key, you can use it 
also when mouse isn’t working as it should),
- Administrator – auca@2020
### Giving window server a static IP
- Windows Key + R (or Click start – Run) – write: 
```
ncpa.cpl
```
(to access network connections) – Right click on Local Area 
connection – properties – Internet Protocol(TCP/IP) – use the 
following IP – IP is `192.168.10.3` – subnet mask is `255.255.255.0`
– default gateway is `192.168.10.1` – primary DNS server is 
`192.168.10.3` – OK – OK.
### Inserting Guest Additions CD
- devices – optical drives – remove disc from virtual drive –
devices – insert guest additions cd image – Next – Next –
Install – Yes – Yes – Continue anyway – Finish – after reboot
### Promoting server from member server to domain controller server
- Windows + R (or Click start-Run)-write: 
```
dcpromo
```
 – Next(*4) – domain name = 
chogm.rw – Next(*7) – Finish – Restart now

### Installing Exchange Server 2003
- Control panel – Add/Remove programs – Add/Remove windows 
components – Tick Applications server – details – tick ASP.NET –
click on Internet Information Services(IIS) – details – Tick FTP 
– Tick SMTP – Tick NMTP – OK – OK – Next( it starts copying) –
(if prompted a window asking you to insert windows CD devices –
remove disc from virtual drive – devices – optical drive –
windows server 2003 – OK) – Finish.
- Devices – remove disc – devices – optical drives – Exchange CD –
(it prompts a window of exchange server – click EXIT) Windows + 
R – write: 
```
D:\setup\i386\setup /forestprep
``` 
Clik OK – Next – I 
agree – Next – wait.
- If done – Windows + R – write: 
```
D:\setup\i386\setup /domainprep
```
Clcik OK – Next – I agree – OK(window notifying that it’s not 
secure)
- If done – Windows + R – write: 
```
D:\setup\i386\setup
```
 Click OK – Next –
... -(Where they require a name with a default name saying First

Organization type the name of your domain e.g.: chogm) - ...-
Finish
### Creating active directory for the domain
- Windows + R: type 
```
dsa.msc
```
 (a command to access active directory)
- Right click on the domain name – new – Organization unit (to 
create a new OU) – type student – Right click student OU – New –
User – First name: type Student – Last name: type 1 – user 
logon name: type Student1 (These names we are using can be 
changed according to the guidelines) – password: type auca@2020 
– tick user cannot change password – tick password never expires 
– Next – Next (Create mailbox). You can create as many OUs you 
want and as many users as you want. (You notice how email is 
configured automatically for each user you create because we 
installed exchange before creating users).
### Deployment of software on the domain using Group Policy 
Management Console (GPMC)
    * Installation of GPMC on windows server 2003
    * Devices – shared folders – shared folders settings – click 
folder adding icon on the far right side in green color –
click down arrow on folder path – choose other path –
choose the folder in which your gpmc and software to deploy 
are saved on physical machine or share the whole local 
disks
    * Open my computer (on VM) – local disk C – create new folder 
called software – right click software – sharing and 
security – share this folder – permissions – remove 
everyone – add – authenticated users(type auth and click 
check names) – add – give permissions according to your 
needs or simply give full control – Apply – OK – click on 
security tab (3rd next to sharing tab) – add – auth(check 
names) – OK – Apply – Full control – Apply – OK – notice 
how the folder now have a hand holding it.
    * On left part click on My network places(if you don’t see it 
click folders on the second line of taskbar of my computer 
near search and back buttons – Entire network – virtualbox 
shared folders - \\vboxsvr – copy the all necessary 
softwares (Mozilla, VLC, Dropbox, GPMC, Putty...) – paste 
them in the folder we created named software.
    * Install GPMC – run GPMC by pressing Windows + R :type
gpmc.msc – Click on the plus sign on forest till you reach 

domain – OUs – right click on student OU – create and link 
a GPO here – name it MOZILLA – create other GPO for VLC and 
DropBox and other software you want to – right click on 
chogm.rw (domain) – create a GPO on it – name it PUTTY –
right click on PUTTY GPO – Edit – on computer configuration 
    * click the plus sign on software – right click software 
package – New – package – on file name write the path don’t 
browse e.g.: \\server\software\putty - open - assigned – ok 
    * on user configuration is the same drill, after writing 
the path – advanced – deployment tab – assigned – tick 
install this application at logon – tick basic – OK. For 
all those softwares you want to deploy it’s same drill. 
When you are done close everything – Windows + R – type: 
gpupdate /force – if it asks for reboot type Y – while 
restarting you can see that it’s installing putty software 
    * Log in XP as one of active directory user – windows + R –
type gpupdate /force – if it asks for reboot/logoff type Y 
    * While restarting you can see that it’s installing 
Mozilla, VLC, Putty,...
