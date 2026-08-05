- a local area network (LAN) is formed when a host is connected to internet that is able to move data to a local network.
- each machine that connects to a network is a host, including a router. 
- The router is connected to internet, this connected called uplink or wide area network *WAN* connection. 
#### Packets
- data transmitted in small chunks called packets. 
	- packets consist of a header and a payload. header has metadata and payload has the application data such as image data or html
#### Network Layers
- functioning network has a network stack. consist of: 
##### Application Layer
- contains language of applications that need to communicate. think of it has the protocol for which two systems use to exchange data
	- i.e. https
	- multiple layers can be combined such as with http and TLS to make https
##### Transport Layer
- defines the data transmission characteristics, data integrity checking, source & destination ports, specification for breaking and assembling to and from packets. 
	- examples: *TCP* Transmission Control Protocol and *UDP* User Datagram Protocol
	- sometimes called the protocol layer
##### Network or Internet Layer
- defines how to move packets from a source host to a destination host. the protocol for this is the *IP* (internet Protocol). 
	- IPV4, IPV6, IPX
##### Physical Layer
- how raw data is sent, ethernet or modem
- sometimes called the link layer or host-to-network layer. 


#### The Internet Layer
- topology of the internet is decentralized. It's made of bunch of interconnected subnets
- a router is able to connect one subnet, to another one (the internet to LAN).
	- routers will have an ip address for each subnet its connected to
- each machine (host) has atleast one ip address. for IPV4 it follows the *dotted quad sequence* a.b.c.d (i.e 10.23.2.37)

##### subnets
-subnets are defined with two pieces: 
- network prefix (aka routing prefix);
- subnet mask (aka nework or routing mask)
###### network prefix
- the quad sequence numbers ie (10.23.2.37)
- 