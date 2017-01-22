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

![](https://cloud.githubusercontent.com/assets/22467856/22185294/34f2d8d0-e0e3-11e6-9fd0-742162888f7e.PNG)


 
2.	Afterwards you will press next and now you have to choose the location to your ISO file

![](https://cloud.githubusercontent.com/assets/22467856/22185314/9ef97db0-e0e3-11e6-8dce-57d73903f3f9.PNG)

it’s common to have it in your download folder. 

3.	Now you want to name your machine

![](https://cloud.githubusercontent.com/assets/22467856/22185331/f18aa61c-e0e3-11e6-8856-7e885587906b.PNG)
 

4.	Choose amount of diskspace is you allow the machine to use 

 
5.	Here you have you have to press on the customize hardware button, and setup what how much memory you want the machine to run with.

![](https://cloud.githubusercontent.com/assets/22467856/22185502/4692fc4c-e0e7-11e6-94ee-3dfb4f9f7b05.PNG)
-	be careful not to give the machine too much power if your machine cant handle it!



6.	Finish, repeat the steps from 1 to 5 for the other devices you want to implement in your topology.
 





5.1 Vmware booting problems with the routers

here is a small guide what to do then SRX router does not want to start.

![](https://cloud.githubusercontent.com/assets/22467856/22185515/a3102652-e0e7-11e6-8760-dd05df905a04.PNG)
 
To start with you will setup your router by doing the advanced option,
and after doing the recommended settings you follow the small guide below.


1.	Open your settings in vmware srx:

![](https://cloud.githubusercontent.com/assets/22467856/22185522/d1b1220e-e0e7-11e6-992b-3148cbafe987.png)

2.	If you do not have any serial ports click to: 









3.	Scroll down until add Serial port and click to ”Next >”

![](https://cloud.githubusercontent.com/assets/22467856/22185527/f646c4a2-e0e7-11e6-8417-da047dfc58b9.png) 

4.	Select”Output to file”

![](https://cloud.githubusercontent.com/assets/22467856/22185537/40fc5ea8-e0e8-11e6-9bb7-09e105f525ba.png)
 




5.	When you need to add your file location, write”test”.

![](https://cloud.githubusercontent.com/assets/22467856/22185557/8a9d74fc-e0e8-11e6-80fa-fd696f4bca63.png) 

6.	 There he goes if you have everything done it should show the following:

![](https://cloud.githubusercontent.com/assets/22467856/22185575/bfe48b8c-e0e8-11e6-837f-73d341674f5a.png)


7.	 Finally, you just check your Router is booting as well:

![](https://cloud.githubusercontent.com/assets/22467856/22185596/02a63754-e0e9-11e6-9d97-5e5614722b76.png) 


 
6.	Basic configuration of the routers
The router has some general setup, like giving it a name and password. First you start with login on the internal router, with “root login”.

![](https://cloud.githubusercontent.com/assets/22467856/22185610/3e0095e2-e0e9-11e6-977a-2f7d6660211c.png)

Then you want to make your own password by go in the edit mode by typing:”cli”

![](https://cloud.githubusercontent.com/assets/22467856/22185619/6172d8aa-e0e9-11e6-8c6d-8aee6e690ae6.png)
 
Now you want to set the hostname for the router.

![](https://cloud.githubusercontent.com/assets/22467856/22185635/b16a403c-e0e9-11e6-824d-18ebdfaf3e2a.PNG)

Note: how the router host name now has become a part of the routers prompt.



Next step is to setup the interfaces on your router by typing the following lines.

![](https://cloud.githubusercontent.com/assets/22467856/22185647/d38d8bb0-e0e9-11e6-8624-d1fff99ff90b.png)




Type then: “show interfaces” to see what interfaces you have now.

![](https://cloud.githubusercontent.com/assets/22467856/22185653/ffebc140-e0e9-11e6-9789-a4a4230f4c29.png)

-------------------------------------------------------------------------------------------------------------

The external router use the same steps but in this case the topology only needs 1 interface for the WEB-server therefore should the last step only be: 

![](https://cloud.githubusercontent.com/assets/22467856/22185664/214f9b72-e0ea-11e6-9edd-695005b75171.png) 
 

7.	Installment of the devices
The devices being described here is the client and the servers. 


7.1	Client

Now you simply install the Client double clicking on the machine and you will just follow the steps which the guide in the disk will ask you to do.
 Please don’t install more devices at once, because that could overheat your pc.


note: remember the passwords!

![](https://cloud.githubusercontent.com/assets/22467856/22185700/a1e60dfc-e0ea-11e6-8105-81627c1d99c0.png)

7.2	WEB server
Now you run the disk like before, and following the steps on the disk itself.

![](https://cloud.githubusercontent.com/assets/22467856/22185727/0b2d135a-e0eb-11e6-9a64-13d5a1ebebe0.png)
 

When you are setup the different servers you must name the servers different to not make any confusion. 

![](https://cloud.githubusercontent.com/assets/22467856/22185735/3642cda0-e0eb-11e6-88f4-eae180e0e2ca.png) 

Under setup on the WEB server you should apply SSH which helps you controlling the devices from the client later in the configuration.
7.3	DNS server

![](https://cloud.githubusercontent.com/assets/22467856/22185762/89444178-e0eb-11e6-882f-7e5234eddbf8.png)

Yet again you will install the server by the disk but, when you meet the section with packages to install you must stop and don’t apply anything. Because you will be able to install the correct things later.

 
8.	Configure Debian Webserver

After you launch your WEB or DNS server it will ask you for a login. The Login is “root” , and the password you typed in the setup.

![](https://cloud.githubusercontent.com/assets/22467856/22185814/bfb46f98-e0ec-11e6-8422-93bf85c85d78.png)
 


Type: “ifconfig”

![](https://cloud.githubusercontent.com/assets/22467856/22185840/40dd61d8-e0ed-11e6-9f7f-88162e7a495f.png)

![](https://cloud.githubusercontent.com/assets/22467856/22185862/645e3fe2-e0ed-11e6-92e4-5f649ae4e959.png) 


User can the information about addresses. Check the address you get in browser. (192.168.0.102)

![](https://cloud.githubusercontent.com/assets/22467856/22187112/1ecdfd32-e101-11e6-909a-c9fb91d107d6.png)

If everything went good the user will get this page.


9.	Setting up DHCP 


Login the server and type the following.

![](https://cloud.githubusercontent.com/assets/22467856/22187144/71adfa02-e101-11e6-9d27-2c88ed73ef0d.png)
 


Then type this to install dhcp server.

![](https://cloud.githubusercontent.com/assets/22467856/22187155/94f83e64-e101-11e6-9df3-9a1edac1b35e.png)
 

When the server finishes the installation.

![](https://cloud.githubusercontent.com/assets/22467856/22187163/b47f8620-e101-11e6-812a-64de5148a91a.png)
 

Scroll down here and change subnet, netmask and range addresses as the server has.

![](https://cloud.githubusercontent.com/assets/22467856/22187172/d8f5dfae-e101-11e6-8c1c-38a431c1a4bb.png)

Save it by pressing CTRL + X and restart your device




10.	Configure SSH for Servers


 Type: “apt-get install openssh-server”.
 
![](https://cloud.githubusercontent.com/assets/22467856/22187181/01832b34-e102-11e6-9fd6-89979f955604.png)

![](https://cloud.githubusercontent.com/assets/22467856/22187191/224dbbc2-e102-11e6-8269-de62146060ff.png)

Go into the following folder:” nano /etc/ssh/sshd_config “

 
In this folde you need to look for the following: “PermitRootLogin” and change it to: “yes “ 

![](https://cloud.githubusercontent.com/assets/22467856/22187201/515c234a-e102-11e6-91d3-35e3dd567678.png)

![](https://cloud.githubusercontent.com/assets/22467856/22187203/56c43eda-e102-11e6-99a4-679c1f4c751c.png)

Log out with pressing CTRL + X and save the modifications.

![](https://cloud.githubusercontent.com/assets/22467856/22187210/a023ffb6-e102-11e6-8e13-705be5f30977.png)

11.	Configure the DNS Server with dnsmasq


Type this to get install dnsmasq into your servers.

![](https://cloud.githubusercontent.com/assets/22467856/22187217/b96dd096-e102-11e6-9c8a-150fe9446ce6.png)

Enable dnsmasq

![](https://cloud.githubusercontent.com/assets/22467856/22187235/d4d8462c-e102-11e6-983c-81d2bf02b37d.png)

Type and going to this location:

![](https://cloud.githubusercontent.com/assets/22467856/22187241/f2c454f0-e102-11e6-97b8-5d6ff69f2b23.png)

Change you dhcp-range for the following: 

![](https://cloud.githubusercontent.com/assets/22467856/22187250/12b4383e-e103-11e6-801b-346776e56cf7.png)

DHCP-Option

![](https://cloud.githubusercontent.com/assets/22467856/22187256/2d9f6722-e103-11e6-9ab5-4579e388f7a8.png)

Set your dhcp-option for the following: ( your address)

![](https://cloud.githubusercontent.com/assets/22467856/22187264/5567ce16-e103-11e6-970c-ab83292a3380.png)

![](https://cloud.githubusercontent.com/assets/22467856/22187269/7a58bcbc-e103-11e6-9948-564b36f0f0dd.png)
up
Delete the hashtag(#) from “log-dhcp”

![](https://cloud.githubusercontent.com/assets/22467856/22187274/8f8b9a00-e103-11e6-83c0-8d4563630712.png)

Do the same with “dhcp-authoritative”

![](https://cloud.githubusercontent.com/assets/22467856/22187277/a4483b74-e103-11e6-9105-f034c3142327.png) 

![](https://cloud.githubusercontent.com/assets/22467856/22187279/aa788f94-e103-11e6-8e6c-240a861196e7.png)

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

![](https://cloud.githubusercontent.com/assets/22467856/22187288/e6858e56-e103-11e6-8e72-b3e54f4c2a07.png) 

2.	Type the following: ping router-int-srvlan
(With this command you are trying to get the connection 

![](https://cloud.githubusercontent.com/assets/22467856/22187294/0821f5e0-e104-11e6-8619-effc5ed0de8a.png)

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

![](https://cloud.githubusercontent.com/assets/22467856/22187319/9a6416fe-e104-11e6-892f-4102cb691e42.png)

•	Get to install it.
•	Open your External Router in Vmware
•	Type the following: ![](https://cloud.githubusercontent.com/assets/22467856/22187326/acfa62fa-e104-11e6-9eeb-3262ca1edd97.png)
•	Then need to fine Local address of the Ext. Router:
![](https://cloud.githubusercontent.com/assets/22467856/22187334/d33cedac-e104-11e6-99b5-91b7dcea1722.png)
•	Open WinSCP

•	Following on next page
•	 

The program needs to get your Local IP, username and password
![](https://cloud.githubusercontent.com/assets/22467856/22187343/f1d3fb66-e104-11e6-8628-e58da5ff71b5.png)

After Login here is the external router root folder.

![](https://cloud.githubusercontent.com/assets/22467856/22187355/279f8210-e105-11e6-897c-a46a4c256e97.png)

•	Open Notepad++:

Import file: router-ext.conf

![](https://cloud.githubusercontent.com/assets/22467856/22187358/469f3a52-e105-11e6-9235-c602d87ea904.png)

Search on: 

Type into the search:206

Its crucially important to switch that Ip address into your one.

After you have done. (In every single line where’s needed )

Copy your file into your ext. Router //root folder

Overwrite it.


Then go back into Vmware/Ext router
Type in: load override  
![](https://cloud.githubusercontent.com/assets/22467856/22187373/7aa17dc4-e105-11e6-8c77-b15314ee9560.png)
Then commit.
Afterwards you can try to ping another router and Let’s see if it is working or not.


13.	Configuring the virtual machines


To connect the devices together you need click right to your servers, routers or your client, open the settings.

![](https://cloud.githubusercontent.com/assets/22467856/22187380/9c335930-e105-11e6-9f0f-73a7c11ca79a.png)

Open LAN Segments:
Add your Globan LAN Segments.
![](https://cloud.githubusercontent.com/assets/22467856/22187398/d9d7ed96-e105-11e6-8d30-9984e45f4b93.png) 


Add your SVRLAN,USRLAN and DMZ and the Connection of the Routers.

![](https://cloud.githubusercontent.com/assets/22467856/22187404/f771b65c-e105-11e6-8c42-33d1382943d1.png)
![](https://cloud.githubusercontent.com/assets/22467856/22187413/1e291b6e-e106-11e6-81d4-b044c2c338e5.png)

Change your Network Adapter from NAT to LAN Segment. (It depends on your server,router or the client)
(See the connections in our Topology)
![](https://cloud.githubusercontent.com/assets/22467856/22187419/454c00ee-e106-11e6-8e5f-7d21d81dc998.png)

Open your Servers and Routers
![](https://cloud.githubusercontent.com/assets/22467856/22187429/612ae6cc-e106-11e6-95d5-a71a1e715ca7.png)

Ping your DNS Server to check the quality of connection.
![](https://cloud.githubusercontent.com/assets/22467856/22187437/822e45bc-e106-11e6-9afc-f9b13b922fe6.png)


Check your IP address by type the following: ifconfig.
![](https://cloud.githubusercontent.com/assets/22467856/22187443/a06f273a-e106-11e6-9b59-4a50674c37c8.png)


Than try to ping it inside your browser:
![](https://cloud.githubusercontent.com/assets/22467856/22187444/a56f3dba-e106-11e6-8e65-2dce22d74663.png)

