what is TCP/IP: 
	- internet protocol - address 
		- has a destination and delivery address like real mail
		- ip is not enough alone to ensure things get delivered
		- bc some servers might be overwhelmed
		- use tcp to solve this.
		- TCP - guarantees the delivery of something.  it sends it in pieces of packets so that if its missing one of them. it requests the missing one. 
		- a TCP also has a port number. 
			- port number designates the sort of message or port that it is requesting. like 
				- http : 80
				- https: 443
- What is a DNS? - domain name server
	- your device asks a local server that asks essential questions for request. kinda like a dictionary or hash table that will give the ip address of  a specific domain name. 
- DHCP - dynamic host protocol - 
	- when you boot your device, it sends out a signal that asks, hey, what server should I use for the DNS requests. 
- HTTP - really its a protocol for a specific way that servers are communicating to each other. a protocol is a two person party that knows how to interact in a client/server relationship. 
html: 

- autofocus="true" - this will autofocus on the box
- essential meta tag for smaller devices: 
	- `<meta name="viewport" content="initial-scale=1, width=device-width">`
	- this sets the viewport of window to width of the device screen so that you dont have massive pages on a small screen.

validator.w3.org - way to validate your own code to make sure that it is correct

Javascript: 
	- useful repeat function: `window.setInterval(fnName, 500)` where the 500 is in miliseconds
- the notes for cs50 includes some more examples of how to use the different listeners for event listeners. 
- 