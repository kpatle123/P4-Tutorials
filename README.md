## p4_programming
### Basic Forwarding using a P4 program 
1. Parse Ethernet and IPV4 from the Packet :
		We are defining two states here for ethernet and ipv4 that will populate ethernet_t and ipv4_t fields.It will extract the information from the headers of ipv4 and ethernet and send it as an output.
 
2.   Ingress Processing:
		In this step when a packet arrives to the switch it will determine the egress port to which the packet need to be forwarded. egress_spec controls which output port a packet will go to. We will deifne an action mark_to_drop(), it has a specific value and such that if egress_spec has that value at the end of ingress processing, the packet will be dropped and not stored in the packet buffer, nor sent to egress processing. Then set the egress port for the next hop and update the ethernet destination address with the address of the next hop. Now update the ethernet source address with the address of the switch and decrement the TTL.
		
3.	 IPV4 lpm Table: 
	 	In this we will read an IPV4 destination address and invoke either drop or ipv4_fowrard. In lpm there is a key-value pair lookup where we give an ipv4 address as a key and this value represents the next hop. An LPM table contains one or more rules, where each rule is a pair of an IP with prefix and a value. If the input key IP matches with more than one rules then the rule with the highest prefix will be used to determine the required value.
  
4.	 Deparser: 
	 	In this stage we are selecting the order in which fields inserted into the outgoing packet.
