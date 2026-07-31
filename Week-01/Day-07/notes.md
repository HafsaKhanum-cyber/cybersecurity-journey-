Day 7   
Wireshark Packet Investigation

Packet Layers

Every packet is divided into different layers.

Frame
↓

Ethernet II
↓

Internet Protocol (IPv4)
↓

Transmission Control Protocol (TCP)
↓

TLS / HTTP / DNS

--------------------------------------------------

Frame

- Arrival Time
- Frame Length

Note

The Frame layer is created by Wireshark during packet capture.
It is not sent across the network.

--------------------------------------------------

Ethernet II

Contains

- Source MAC Address
- Destination MAC Address
- EtherType

MAC Address

A MAC Address is the physical address of a network interface.

It is only used inside a Local Area Network (LAN).

Practical

Run:

ip a

Does the Source MAC Address match your MAC Address?

Answer:

yes
--------------------------------------------------

IPv4

Contains

- Source IP
- Destination IP
- TTL
- Protocol

TTL (Time To Live)

TTL is a hop counter.

Every router decreases the TTL by 1.

If TTL becomes 0, the packet is discarded.

Practical

TTL Value:

64

Why is TTL important?

Answer:

its important to know the hops of each packet

--------------------------------------------------

TCP

Contains

- Source Port
- Destination Port
- Sequence Number
- Acknowledgment Number
- Window Size
- Flags

Sequence Number

Keeps packets in the correct order.

Window Size

Controls how much data can be sent before waiting for an acknowledgment.

Question

Why does TCP use Sequence Numbers?

Answer:
to know if there are any missing packets

--------------------------------------------------

Display Filters

Filter

ip.addr == YOUR_IP

Observation

shows all packets related to my computer either source or destination 

--------------------------------------------------

Filter

tcp.port == 443

observation

Shows HTTPS/TLS traffic.

--------------------------------------------------

Filter

dns.qry.name == "google.com"

observation

Shows DNS requests for Google.


--------------------------------------------------

Follow TCP Stream

Right Click Packet

↓

Follow

↓

TCP Stream

Purpose

Shows the complete communication between two devices.

Questions

Which IP addresses communicated?

Answer:

its uing 443 everything is encrytped

--------------------------------------------------

Statistics

Statistics

↓

Conversations

Highest packet count:

79

Statistics

↓

Protocol Hierarchy

Most common protocol:

tcp 100 percent and tls 62 percent 
tcp is the highest

--------------------------------------------------

SOC Investigation

Scenario

A user cannot access GitHub.

Packet Capture shows:

- DNS Query
- DNS Response
- SYN
- SYN ACK
- ACK

GitHub still does not load.

What would you investigate next?

Answer:

firewall 
