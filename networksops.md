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

#### traceroute
- Network troubleshooting utility, shows number of hops to destination
- Determines path traveled

```bash
$ traceroute google.com

traceroute to google.com (216.58.195.78), 30 hops max, 60 byte packets
 1  10.0.1.1 (10.0.1.1)  1.654 ms  1.595 ms  1.569 ms
 2  gw-200paulnorth-v302.static.monkeybrains.net (199.116.72.65)  4.950 ms  4.944 ms  4.932 ms
 3  172.17.17.212 (172.17.17.212)  4.923 ms  4.912 ms  4.909 ms
 4  172.17.17.236 (172.17.17.236)  4.883 ms  6.176 ms  6.187 ms
 5  172.17.17.235 (172.17.17.235)  8.306 ms  8.301 ms  8.293 ms
 6  172.17.19.218 (172.17.19.218)  8.218 ms  7.689 ms  7.634 ms
 7  172.17.18.50 (172.17.18.50)  6.526 ms  11.045 ms  11.023 ms
 8  lemon.lemon-mosca-10GB.core.monkeybrains.net (208.69.43.185)  10.235 ms  10.252 ms  10.246 ms
 9  206.41.106.63 (206.41.106.63)  10.194 ms  10.194 ms  13.807 ms
10  108.170.242.241 (108.170.242.241)  13.629 ms 108.170.242.81 (108.170.242.81)  13.627 ms  13.558 ms
11  108.170.235.239 (108.170.235.239)  10.858 ms  10.818 ms 108.170.235.237 (108.170.235.237)  6.713 ms
12  sfo07s16-in-f14.1e100.net (216.58.195.78)  7.398 ms  7.407 ms  8.360 ms
```

#### netstat
- Network Statistic displays connection info
- Can display connections, routing table info
- `-r` displays routing table info

```bash
$ netstat -r

Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
default         10.0.1.1        0.0.0.0         UG        0 0          0 wlp2s0f0
10.0.0.0        *               255.255.254.0   U         0 0          0 wlp2s0f0
link-local      *               255.255.0.0     U         0 0          0 wlp2s0f0
```

#### dig
- Domain Information Groper
- query DNS information, used to troubleshoot DNS related queries
- More info [here](https://www.tecmint.com/10-linux-dig-domain-information-groper-commands-to-query-dns/)

```bash
$ dig www.google.com

; <<>> DiG 9.10.3-P4-Ubuntu <<>> www.google.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 59323
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;www.google.com.			IN	A

;; ANSWER SECTION:
www.google.com.		36	IN	A	172.217.6.68

;; Query time: 35 msec
;; SERVER: 127.0.1.1#53(127.0.1.1)
;; WHEN: Mon Sep 11 16:21:30 PDT 2017
;; MSG SIZE  rcvd: 59
```

#### nslookup
- Command used to query internet domain name servers
- DNS related queries
- Shows records (IP Addresses)

```bash
$ nslookup www.google.com

Server:		127.0.1.1
Address:	127.0.1.1#53

Non-authoritative answer:
Name:	www.google.com
Address: 172.217.6.68

```

#### route
- shows and manipulates *ip* routing table
- `route` shows routing table
- `route add -net 10.10.10.0/24 gw 192.168.0.1`
- `route del -net 10.10.10.0/24 gw 192.168.0.1`
- `route add default gw 192.168.0.1` adds a default gateway

#### host
- host command finds IP address, and queries DNS records
- `-t` argument finds DNS resource records

```bash
$ host google.com

google.com has address 216.58.194.206
google.com has IPv6 address 2607:f8b0:4005:809::200e
google.com mail is handled by 50 alt4.aspmx.l.google.com.
google.com mail is handled by 40 alt3.aspmx.l.google.com.
google.com mail is handled by 10 aspmx.l.google.com.
google.com mail is handled by 30 alt2.aspmx.l.google.com.
google.com mail is handled by 20 alt1.aspmx.l.google.com.

$ host -t A google.com

google.com has address 172.217.6.46
```

#### arp
- Address Resolution Protocol
- View kernel's ARP tables

#### iwconfig
- Wireless network interface
- Similar to ifconfig, can set SSID channel, encryption

Info from:
- Wikipedia
- [Tecmint Linux Network/Troubleshooting](https://www.tecmint.com/linux-network-configuration-and-troubleshooting-commands/)
- [Tecmint Linux Advanced](https://www.tecmint.com/20-advanced-commands-for-linux-experts/)
