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
- within the quad sequence (10.23.2.37) the network prefix are those numbers that all hosts in the subnet have in common
	- for example if you have the above and 10.23.2.50, they both share the network prefix of 10.23.2
###### subnet mask
- if you run `ip address show` you'll see something like: `inet 10.23.2.10/24` 
	- above represents the whole combination of network prefix and subnet mask
	- inet is ipv4 and the `/24` is the subnet mask that all the hosts in the subnet will have in common. the 24 comes from the sequence of bits (translates to 255.255.255.0) which is 3 sets of 8bits, equaling 24. 24 is the shorthand
		- in binary looks like: 1111111 1111111 11111111 0000000 (24 1 bit sequence)
	- /24 is the most common subnet mask for local end-user networks

##### Routes and kernel routing table
- to put all together, for example, host A ( a linux mahine ) with ip address of 10.23.2.4 is connected at local network at address 10.23.2.0/24. it can access the internet by communicating with router host at 10.23.2.1
- The kernel will choose a route based on the longest destination prefix that matches. 
	- a default gateway is 0.0.0.0/0 which matches anything but its prefix length is 0 bits, vs something else that has more bit length match, that will be preferred. 