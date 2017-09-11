# Network Notes

### OSI Model

Layer Name | Description | Examples
-|-|-
Physical | Physical medium, transmission material, raw bit streams | Wires, wireless, transmission lines, Ethernet, 802.11 protocols, network hardware
Data Link | node to node data link, flow control | MAC (Media Access Control) layer - how devices gain access to medium and permission to transmit, LLC (Logical link control) layer - identifying network protocols, error checking, frame synchronization
Network | functional and procedural means of transferring datagrams from nodes to other nodes in a network, deals with routing | Routing protocols, IP, ICMP, ISPF, RIP
Transport | protocols for transmitting datagrams to a destination through networks, QoS functionality | TCP, UDP
Session | manages connection between nodes on network, initiates, manages, terminates connections (sessions/conversations) | Sockets, TCP session
Presentation | establishes context between application layer and session protocol data, transforms data into format for application | MIME, SSL, serialization of data
Application | layer closest to the user, determines identity and availability of communication partners | BGP, DNS, FTP, DHCP
