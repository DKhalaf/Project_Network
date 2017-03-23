# Project_Network
## I've created a project network where my goal was to establish connection between 5 devices, and be able to access the internet. I made this recovery plan in case things might go wrong. This recovery plan is tested, and working as it should. Be aware that once you start working on your Ubuntu client, you might need to update, upgrade etc..., before you can run some commands. Other than that, you're good to go.


## This is the project I've made:
![layer3](https://cloud.githubusercontent.com/assets/23449056/24168149/877b2c38-0e79-11e7-8264-0df89d26b36b.png)



## Before we start, here's some info
* Requirements: VMWare - SRX Router - Ubuntu Desktop(client) - Web-Server - DNS-server

/////////////////////////////////////////////////////////////////////////////////////////////////////////

## Installation
1) Download and install in VMWare, a Ubuntu client from https://www.ubuntu.com/download/desktop
2) Download and install in VMWare, a Debian linux server from: https://www.debian.org/
3) Download and install in VMWare, a SRX Router. (can be found on fronter or https://www.juniper.net

### After installing the router, remember to configure hostname and password for both
4) Clone the SRX Router in VMWare. Name one router, Router-INT and the other Router-EXT
5) Open Router-INT, go to edit mode, type:
   set interfaces ge-0/0/0.0 family inet address 192.168.0.1/24
6) Open Router-EXT, go to edit mode, type: 
    set interfaces ge-0/0/0.0 family inet address 10.0.1.1/24
7) commit both routers

## Setting up internet connection for Ubuntu Client
8) IN VMWare right click Ubuntu client -> Settings -> Network Adapter -> choose: NAT, click OK
* Verify that you have internet connection now. Open terminal, type: ping 8.8.8.8

## Cloning Project_Network, github repository from Ubuntu client

9) Open terminal on client and type: sudo apt install git
10) Open terminal on client and type: git clone https://github.com/DKhalaf/Project_Network
![gitclone](https://cloud.githubusercontent.com/assets/23449056/24166163/b4bd5556-0e72-11e7-8e4b-8539889bd8cd.PNG)

## Downloading, installing and enabling SSH(Secure Shell) in Ubuntu client
11) Open terminal on client and type: sudo apt-get install ssh
12) Open terminal on client and type: sudo update-rc.d ssh enable
13) Open terminal on client and type: sudo service ssh start


## Setting up communication between client and routers
14) Go to VMWare, right click Router INT -> Settings -> NAT -> click OK
15) Go to VMWare, right click Router EXT -> Settings -> NAT -> click OK
* Now both your routers should be able to ping 8.8.8.8


## Router-INT: Pushing router configuration files to the routers
### Reffering to step 5, copy the IP Address of your Router INT so we can push the configuration files
### Following command will be used: scp *router configuration file location* root@*ip of your router*:~srxfile.conf

16) Open terminal on client and type: scp -r Project_Network/Routers/ROUTER-INT root@192.168.0.1:~/Router-INT.conf
* Remember to use the IP Address that you had given your interface!
17) Open Router-INT. In edit mode, type: load override INT.conf
18) commit
## Router-EXT: Pushing router configuration file to the router
### Reffering to step 5, copy the IP Address of your Router EXT so we can push the configuration file
### Following command will be used: scp *router configuration file location* root@*ip of your router*:~srxfile.conf

19) Open terminal on client and type: scp -r Project_Network/Routers/ROUTER-EXT root@10.0.1.1:~/Router-EXT.conf
* Remember to use the IP Address that you had given your interface!
20) Open Router-EXT. In edit mode, type: load override EXT.conf
21) commit

/////////////////////////////////////////////////////////////////////////////////////////////////////////
# Setting up connection between devices in VMWare 
#### Open VWWare -> Edit -> Virtual Network Editor -> VMNet 8(NAT) -> Change settings ->  Subnet IP: 10.0.0.0 and Subnet mask: 255.255.255.0
![networkeditor](https://cloud.githubusercontent.com/assets/23449056/24166167/b81587be-0e72-11e7-96ce-edfd166a4beb.PNG)


#### Now change adapter settings on all your devices!
* Right click Ubuntu Client -> Settings -> Network Adapter -> Lan Segments... -> Add -> URSLAN -> click OK
* Right click Router-INT -> Settings -> Network Adapter -> Lan Segment -> URSLAN -> click OK
* Right click Router-INT -> Settings -> Network Adapter 2 -> Lan Segments... -> Add -> SVRLAN -> click OK
* Right click Router-INT -> Settings -> Network Adapter 3 -> Lan Segments... -> Add -> RouterConnection -> click OK
* Right click Router-EXT -> Settings -> Network Adapter -> Lan Segment -> RouterConnection -> click OK
* Right click Router-EXT -> Settings -> Network Adapter 2 -> Lan Segments... ->ADD -> DMZ -> click OK
* Right click Router-EXT -> Settings -> Network Adapter 3 -> Lan Segment -> NAT -> click OK
* Right click DNS-Server -> Settings -> Network Adapter  -> Lan Segment -> SVRLAN -> click OK
* Right click Web-Server -> Settings -> Network Adapter  -> Lan Segments -> DMZ -> click OK

##### For all the network adapters you use for each device, remember to mark "Connect at power on". -Remove the mark on the other adapters that you dont use!
![devicestatus](https://cloud.githubusercontent.com/assets/23449056/24166451/96993ad0-0e73-11e7-9c12-47d12e5a44b0.PNG)

# Login and Passwords
* For all devices
##### username: root
##### password: PN123456


# DNS-Server & Web-Server configuration
Set these settings up for your servers. To edit, login and type: nano /etc/network/interfaces
* DNS-Server
![dns](https://cloud.githubusercontent.com/assets/23449056/24170537/82f47432-0e81-11e7-93a6-b4f5bc87b04c.PNG)

* Web-Server
![webserver](https://cloud.githubusercontent.com/assets/23449056/24170543/862aee56-0e81-11e7-86e3-490824441799.PNG)


