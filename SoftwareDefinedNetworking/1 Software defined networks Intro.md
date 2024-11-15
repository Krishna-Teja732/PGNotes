
### 1. Introduction
- SDN is an approach to build and manage networks
#### 1.1 Issues with traditional networks
- Networks have various devices such as routers, switches, firewalls
- The interface to configure each device varies, this makes it complex to configure a large network with multiple devices
- #TODO What are some examples for configuring a network device?

#### 1.2 Approach in SDN 
- Separate control plane and data plane
- Consolidate control plane, such that control plane manages multiple data planes using a **Southbound API** (example: Open Flow)
- **What is a control plane and data plane?**
	- **Control plane:** 
		- The actions that decide how the data should be forwarded in the network
		- The control plane affects the data plane
		- The control plane does not carry and data of the hosts in the network. (i.e. it is an overhead that is required to make the network function)
		- Example: Constructing the routing table
	- **Data plane:** 
		- The decision to forward packets to next interface is performed in the data plane 
		- Here the packets forwarded belong to the hosts in the network
		- How is the next interface determined? This is the responsibility of the control plane
		- For example: 
			- Dropping packets based on a protocol will be done in the data plane
			- Forwarding the packet to the appropriate interface
#### 1.3 Early work on programmable networks 
- **Active Networking**
	- Approach in active networking 
		- Control the network using an API
		- Network nodes expose resources using APIs(Example resources: processing, storage, queues)
		- Using these API, create custom behaviour for packets
	- Active networking focused on data plane programmability
- **Separating Control plane and data plane**
	- Need: Control the paths that deliver data(traffic engineering)
	- Issue: Traditional routers had the control and data plane tightly coupled. Means to control the path were primitive( #TODO how was the path controlled in traditional networks)
	- Approach: Logically centralized control plane and data plane communicate through a standard API
- **Open flow and Network OS**
	- **Open flow** switch contains Table of packet handling rules 
		- **Rule pattern:** compare the first bits of the packet and rule pattern, if patter matches apply the rule action
		- **Rule action:** action performed on packet(example: drop, forward, flood, send to controller)
		- **Counters:** To tract number of bytes and packets 
		- **Priority:** Each rule will have a priority to prevent ambiguity when two patterns match
	- What happens when a packet reaches a open flow switch
		- Match the bits of the packet with the rules
		- If multiple rules match, perform the action of the highest priority rule
		- Update counters for the rule executed
	- **Network OS**
		- Distributed controllers that act as a single logical controller.
		- This requires network state info and means for network state management.
		- The network OS manages the network state information. The logical controller can use this info rather than dealing with the complexity of collecting this info
		- The network controllers communicate with the network OS using a **Northbound API**