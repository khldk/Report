Recovery documentation


Project network

Group 5
	

Autumn 2016















 
![](https://cloud.githubusercontent.com/assets/22467856/22125747/356cbf06-de95-11e6-9eef-291cfa2a58ec.jpg)

Lillebaelt Academy of
University of applied sciences


IT Technology



Authors:
Milan Vince: mila1025@edu.eal.dk

Kevin Herhold Larsen: kevi2901@edu.eal.dk

Rickie Ljungberg: rick0118@edu.eal.dk

Michal Skórczewski: mich74p0@edu.eal.dk

Ali Abed Chayed: @edu.eal.dk



  
Table of context

1.	Introduction	2
2.	Overview	3
3.	Files which are needed	3
4.	Layer 3 Diagram	4
5.	How to create virtual machines	5
5.1 Vmware booting problems with the routers	9
6.	Basic configuration of the routers	13
7.	Installment of the devices	16
7.1	Client	16
7.2	WEB server	17
7.3	DNS server	18
8.	Configure Debian Webserver	19
9.	Setting up DHCP	21
10.	Configure SSH for Servers	21
11.	Configure the DNS Server with dnsmasq	22
Sources	25
12.	What will be included in this document in next version.	25
13.	Configuring the virtual machines	26




 
1.	Introduction

The document describes the steps how to create “Project Network” which has:

1 client 
2 routers (internal + external)
2 servers (WEB- and DNS server)
![](https://cloud.githubusercontent.com/assets/22467856/22183844/82c8ec0a-e0c7-11e6-96f6-4b7529507425.png)
You will not be able to follow the guideline if you don’t have installed: 
VMware workstation Pro 12 click on the link to get to the homepage and start download by click on downloads on the left side, and choose your OS.

 
 
2.	Overview

•	Files which are needed
•	Level 3 Diagram
•	Vmware booting problems with the routers
•	How to create virtual machines and install
•	Basic configuration of the routers 
•	Installment of the devices (e.x Web Server)
•	Setting up DHCP 
•	Setting up SSH for Server 
•	Sources
•	Check your DNS server
•	External Router Config
•	Configuring the virtual machines







3.	Files which are needed

In these section the plan shows which sources are needed to make the recover:

•	Router: JunOS SRX VMWare virtual machine OVF 
(For EAL students, login Fronter, go in the data communication folder, go in folder called software and click on the arrow down left beside the filename and download)

•	Router: JunOS SRX VMWare virtual machine VMDK 
(same as the previous file)

•	Server: Debian net installer ISO (download)

•	Client: Ubuntu 16.04.1 LTS (Client) (download)

•	Ext. Router.conf file


 
4.	Layer 3 Diagram

This level 3 diagram show the solution and giving a point of view how will the Topology looks like:
![](https://cloud.githubusercontent.com/assets/22467856/22185253/613c4332-e0e2-11e6-9f62-37b9cbf41d49.png)


 
5.	How to create virtual machines 

When you have your VMware up and running you will do following to install a virtual machine, which can be any devices:

1.	When the program is running you will create a virtual machine, by pressing on that box you will get this window


 
2.	Afterwards you will press next and now you have to choose the location to your ISO file

it’s common to have it in your download folder. 

3.	Now you want to name your machine
 


4.	Choose amount of diskspace is you allow the machine to use 

 
5.	Here you have you have to press on the customize hardware button, and setup what how much memory you want the machine to run with.

-	be careful not to give the machine too much power if your machine cant handle it!



6.	Finish, repeat the steps from 1 to 5 for the other devices you want to implement in your topology.
 





5.1 Vmware booting problems with the routers

here is a small guide what to do then SRX router does not want to start.

 
To start with you will setup your router by doing the advanced option,
and after doing the recommended settings you follow the small guide below.


1.	Open your settings in vmware srx:


2.	If you do not have any serial ports click to: 









3.	Scroll down until add Serial port and click to ”Next >”
 
4.	Select”Output to file”

 




5.	When you need to add your file location, write”test”.
 
6.	 There he goes if you have everything done it should show the following:
 







7.	 Finally, you just check your Router is booting as well:
 


 
6.	Basic configuration of the routers
The router has some general setup, like giving it a name and password. First you start with login on the internal router, with “root login”.
 
Then you want to make your own password by go in the edit mode by typing:”cli”
 
 
Now you want to set the hostname for the router.
 
Note: how the router host name now has become a part of the routers prompt.



Next step is to setup the interfaces on your router by typing the following lines.
 




Type then: “show interfaces” to see what interfaces you have now.
 
-------------------------------------------------------------------------------------------------------------

The external router use the same steps but in this case the topology only needs 1 interface for the WEB-server therefore should the last step only be: 
 
 


 
7.	Installment of the devices
The devices being described here is the client and the servers. 


7.1	Client

Now you simply install the Client double clicking on the machine and you will just follow the steps which the guide in the disk will ask you to do.
 Please don’t install more devices at once, because that could overheat your pc.


note: remember the passwords!
 

 
7.2	WEB server
Now you run the disk like before, and following the steps on the disk itself.

 

When you are setup the different servers you must name the servers different to not make any confusion. 
 

Under setup on the WEB server you should apply SSH which helps you controlling the devices from the client later in the configuration.
7.3	DNS server

Yet again you will install the server by the disk but, when you meet the section with packages to install you must stop and don’t apply anything. Because you will be able to install the correct things later.

 
8.	Configure Debian Webserver

After you launch your WEB or DNS server it will ask you for a login. The Login is “root” , and the password you typed in the setup.

 




 

Type: “ifconfig”

 



User can the information about addresses. Check the address you get in browser. (192.168.0.102)


 




If everything went good the user will get this page.







9.	Setting up DHCP 





Login the server and type the following.

 


Then type this to install dhcp server.



 

When the server finishes the installation.

 

Scroll down here and change subnet, netmask and range addresses as the server has.

Save it by pressing CTRL + X and restart your device




10.	Configure SSH for Servers


 

Type: “apt-get install openssh-server”.
 


Go into the following folder:” nano /etc/ssh/sshd_config “

 
In this folde you need to look for the following: “PermitRootLogin” and change it to: “yes “ 
Log out with pressing CTRL + X and save the modifications.
 

11.	Configure the DNS Server with dnsmasq


Type this to get install dnsmasq into your servers.
 
Enable dnsmasq

Type and going to this location:
 
Change you dhcp-range for the following: 

DHCP-Option
 
Set your dhcp-option for the following: ( your address)
 

 
up
Delete the hashtag(#) from “log-dhcp”
 
Do the same with “dhcp-authoritative”
 
 
Press CTRL + X and save modifications of your folder. 
Sources

Group 7

https://github.com/deadbok/project_network

Juniper vSRX Router Installation

https://fronter.com/eal/links/files.phtml/2080432588$548107012$/1st+Semester/Data+Communication/Literature/Juniper+and+Virtual+Box+GNS+SRX+configuration+V07.pdf









12.	What will be included in this document in next version.
•	Set static ips on the servers













Check your DNS server

In the following steps you will learn how to check if your DNS server working. You will need the following devices to run:
•	Internal Router
•	External Router
•	Client (Ubuntu)
•	DNS

1.	Open terminal in your Client
 

2.	Type the following: ping router-int-srvlan
(With this command you are trying to get the connection 

If it is able to ping it means DNS Server is working.











External Router Config
In the following step you will see the Guide how to configure your External router from the beginning:

Step 1:Get SSH for your Ext. Router

#Enter the cli
cli

#Enter edit mode
edit

# Set the root password
set system root-authentication plain-text-password
New Password: type password here
Retype new password: retype password here

# Set the interface to DHCP
set interfaces ge-0/0/3 unit 0 family inet dhcp

# Put the interface in the trusted zone and allow all services
set security zones security-zone trust interfaces ge-0/0/3.0 host-inbound-traffic system-services all

# Allow all protocols
set security zones security-zone trust interfaces ge-0/0/3.0 host-inbound-traffic protocols  all

# Commit the changes
commit
Step 2: Download WinSCP: https://winscp.net/eng/download.php 
•	Get to install it.
•	Open your External Router in Vmware
•	Type the following: 
•	Then need to fine Local address of the Ext. Router:

•	Open WinSCP

•	Following on next page
•	 

The program needs to get your Local IP, username and password
 

After Login here is the external router root folder.




•	Open Notepad++:

Import file: router-ext.conf 
Search on: 

Type into the search:206

Its crucially important to switch that Ip address into your one.

After you have done. (In every single line where’s needed )

Copy your file into your ext. Router //root folder

Overwrite it.


Then go back into Vmware/Ext router
Type in: load override  


Then commit.
Afterwards you can try to ping another router and Let’s see if it is working or not.















13.	Configuring the virtual machines


 

To connect the devices together you need click right to your servers, routers or your client, open the settings.















 


Open LAN Segments:
Add your Globan LAN Segments.
 


Add your SVRLAN,USRLAN and DMZ and the Connection of the Routers.



 



 

Change your Network Adapter from NAT to LAN Segment. (It depends on your server,router or the client)
(See the connections in our Topology)

 





Open your Servers and Routers



 

Ping your DNS Server to check the quality of connection.



 

Check your IP address by type the following: ifconfig.














Than try to ping it inside your browser:

 


