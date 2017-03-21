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

## CLONING GITHUB REPOSITORY

Right click your ubuntu client in VMWare, go to Network Adapter, choose "NAT"
You should be able to access the internet on your ubuntu client. Ping 8.8.8.8 from terminal to verify.

Open terminal on client and type: sudo apt install git

Open terminal on client and type: git clone https://github.com/DKhalaf/Project_Network

Open Router-INT. In edit mode, type: show interfaces
