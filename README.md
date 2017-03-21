# Project_Network Recovery Plan

![layer3](https://cloud.githubusercontent.com/assets/23449056/24164533/56deaea2-0e6e-11e7-913f-94d309edbb3b.png)

* Requirements: VMWare - SRX Router - Ubuntu Desktop(client) - Web-Server - DNS-server

/////////////////////////////////////////////////////////////////////////////////////////////////////////

## Installation
1) Download and install in VMWare, a Ubuntu client from https://www.ubuntu.com/download/desktop
2) Download and install in VMWare, a Debian linux server from: https://www.debian.org/
3) Download and install in VMWare, a SRX Router. (can be found on fronter or https://www.juniper.net)

### After installing the router, remember to configure hostname and password for both
4) Clone the SRX Router in VMWare. Name one router, Router-INT and the other Router-EXT
5) Give both routers an IP-Address on interface ge-0/0/0

## Setting up internet connection for Ubuntu Client
6) IN VMWare right click Ubuntu client -> Settings -> Network Adapter -> choose: NAT, click OK
* Verify that you have internet connection now. Open terminal, type: ping 8.8.8.8

## Cloning Project_Network, github repository from Ubuntu client

7) Open terminal on client and type: sudo apt install git
8) Open terminal on client and type: git clone https://github.com/DKhalaf/Project_Network


## Downloading, installing and enabling SSH(Secure Shell) in Ubuntu client
9) Open terminal on client and type: sudo apt-get install ssh
10) Open terminal on client and type: sudo update-rc.d ssh enable
11) Open terminal on client and type: sudo service ssh start


## Setting up communication between client and routers
12) Go to VMWare, right click Router INT -> Settings -> NAT -> click OK
13) Go to VMWare, right click Router EXT -> Settings -> NAT -> click OK
* Now both your routers should be able to ping 8.8.8.8


## Router-INT: Pushing router configuration files to the routers
### Reffering to step 5, copy the IP Address of your Router INT so we can push the configuration files
### Following command will be used: scp *router configuration file location* root@*ip of your router*:~srxfile.conf

14) Open Router-INT. In edit mode, type: show interfaces
15) Open terminal on client and type: scp Project_Network/Routers/ROUTER-INT root@192.168.0.1:~/INT.conf
* Remember to use the IP Address that you had given your interface!
16) Open Router-INT. In edit mode, type: load override srxfile.conf

## Router-EXT: Pushing router configuration file to the router
### Reffering to step 5, copy the IP Address of your Router EXT so we can push the configuration file
### Following command will be used: scp *router configuration file location* root@*ip of your router*:~srxfile.conf

17) Open Router-EXT. In edit mode, type: show interfaces
18) Open terminal on client and type: scp Project_Network/Routers/ROUTER-EXT root@192.168.0.2:~/EXT.conf
* Remember to use the IP Address that you had given your interface!
19) Open Router-EXT. In edit mode, type: load override srxfile.conf


/////////////////////////////////////////////////////////////////////////////////////////////////////////
# Setting up connection between devices in VMWare
* Right click Ubuntu Client -> Settings -> Network Adapter -> Lan Segments... -> Add -> URSLAN -> click OK

* Right click Router-INT -> Settings -> Network Adapter -> Lan Segment -> URSLAN -> click OK
* Right click Router-INT -> Settings -> Network Adapter 2 -> Lan Segments... -> Add -> SVRLAN -> click OK
* Right click Router-INT -> Settings -> Network Adapter 3 -> Lan Segments... -> Add -> RouterConnection -> click OK

* Right click Router-EXT -> Settings -> Network Adapter -> Lan Segment -> RouterConnection -> click OK
* Right click Router-EXT -> Settings -> Network Adapter 2 -> Lan Segments... ->ADD -> DMZ -> click OK
* Right click Router-EXT -> Settings -> Network Adapter 3 -> Lan Segment -> NAT -> click OK

* Right click DNS-Server -> Settings -> Network Adapter  -> Lan Segment -> SVRLAN -> click OK

* Right click Web-Server -> Settings -> Network Adapter  -> Lan Segments -> DMZ -> click OK

#### For all the network adapters you use for each device, remember to mark "Connect at power on". -Remove the mark on the other adapters that you dont use!


