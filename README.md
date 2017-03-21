# Project_Network Recovery Plan

* Requirements:
VMWare - SRX Router - Ubuntu Desktop(client) - Webserver - DNS-server

1) Download and install in VMWare, a ubuntu client from https://www.ubuntu.com/download/desktop
2) Download and install in VMWare, a debian linux server from: https://www.debian.org/
3) Download and install in VMWare, a SRX router and clone it. (can be found on fronter or https://www.juniper.net)

Communication between devices and internet access



SRX ROUTERS:
4) Name one router, Router-INT and the other Router-EXT
5) Give both routers an IP-Address on interface ge-0/0/0

CLONING GITHUB REPOSITORY
6) Right click your ubuntu client in VMWare, go to Network Adapter, choose "NAT"
You should be able to access the internet on your ubuntu client. Ping 8.8.8.8 from terminal to verify.
7) Open terminal on client and type: sudo apt install git
8) Open terminal on client and type: git clone https://github.com/DKhalaf/Project_Network
9) Open Router-INT. In edit mode, type: show interfaces
10) 
