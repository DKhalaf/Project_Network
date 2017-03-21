# Project_Network Recovery Plan
* Requirements: VMWare - SRX Router - Ubuntu Desktop(client) - Webserver - DNS-server

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

## Pushing router configuration file
#### Remeber step 5? Lets use the IP-Addresses that you had given your both routers on interface ge-0/0/0
9) Open Router-INT. In edit mode, type: show interfaces
