# Network/Ops Notes

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

### Network Config / Troubleshooting

#### ifconfig
- Interface configurator
- Initializes interfaces, enable/disable
- Assign IP address to interfaces
- Can be used to view IP address, hardware, MAC Address

```bash
$ ifconfig wlp2s0f0

wlp2s0f0  Link encap:Ethernet  HWaddr 10:08:b1:ae:1a:fd  
          inet addr:10.0.0.248  Bcast:10.0.1.255  Mask:255.255.254.0
          inet6 addr: fe80::1b2c:326:8ccb:9066/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:5173060 errors:0 dropped:0 overruns:0 frame:0
          TX packets:2887688 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:6255171647 (6.2 GB)  TX bytes:363263759 (363.2 MB)
```

- `ifup eth0` enables eth0 interface
- `ifdown eth0` disables eth0
- `ifconfig eth0 192.168.50.5 netmask 255.255.255.0` assigns IP and gateway
- changed config resets on reboot

#### ping
- Packet INternet Groper
- Uses ICMP suite to communicate
- `-c` argument specifies ping count, otherwise repeats until interrupt

```bash
$ ping -c 5 google.com
PING google.com (216.58.194.174) 56(84) bytes of data.
64 bytes from sfo07s13-in-f174.1e100.net (216.58.194.174): icmp_seq=1 ttl=52 time=6.69 ms
64 bytes from sfo07s13-in-f174.1e100.net (216.58.194.174): icmp_seq=2 ttl=52 time=8.19 ms
64 bytes from sfo07s13-in-f174.1e100.net (216.58.194.174): icmp_seq=3 ttl=52 time=8.72 ms
64 bytes from sfo07s13-in-f174.1e100.net (216.58.194.174): icmp_seq=4 ttl=52 time=7.91 ms
64 bytes from sfo07s13-in-f174.1e100.net (216.58.194.174): icmp_seq=5 ttl=52 time=7.24 ms

--- google.com ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4006ms
rtt min/avg/max/mdev = 6.698/7.755/8.722/0.721 ms

```
