
### ACN
- How does a process know weather to ignore or use the ICMP packet
	- There are many ICMP messages sent to a host. When using raw sockets, all ICMP messages can be received by the socket. 
	- Let say there are two process communicating with a single server. One of the processes used the wrong port, this will give a ICMP type 3 code 3 error. Both client process raw sockets will receive this ICMP message.
	- How does the process know this message is intended for it?