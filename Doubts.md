
### ACN
- How does a process know weather to ignore or use the ICMP packet
	- There are many ICMP messages sent to a host. When using raw sockets, all ICMP messages can be received by the socket. 
	- Let say there are two process communicating with a single server. One of the processes used the wrong port, this will give a ICMP type 3 code 3 error. Both client process raw sockets will receive this ICMP message.
	- How does the process know this message is intended for it?
- When running a single threaded TCP server, what happens when two client connect at the same time?
	- Observed Trend: Even if the server does not execute the accept call for the second client, the client connect function returns 0(i.e. successfully connected to the server). This make the client timeout in the recv() function to the server 