day 4 

part 1 =theory
*ip address=address of every computer
*ipv4 =containts 32 bits ,each one is octet 
*private and public ips=

the router has public ip and our home devices private ips too but it only shows public ip to the internet to communicate the lp of my house connects with private ip and the router tranlates it or converts it into public ip and contacts with internet and then again comes to my laprop 

*common private ips 
10.0.0.0 – 10.255.255.255

172.16.0.0 – 172.31.255.255

192.168.0.0 – 192.168.255.255

*subnet mask=
subnet mask identifies the 2 parts of ip address the host and network 
so subnet mask automatically identifies the both part and tell where required like dns work no human work needed 

DNS and the subnet mask have different jobs, but they are similar because both work automatically in the background to help your computer communicate over a network.

*/24 means= the first 24 bits are the network part.
  /24 is the same as 255.255.255.0.

part 2=linux practical 

COMMANDS

Run:

1=ip a

Questions:

What is your IP address?
Do you see /24?
Which interface has the IP?

answers=
192.168.1.107
yes 
wlp1so

2=ip route 

Questions:

What is your default gateway?
Which interface is used?

Answers
via 192.168.1.1
wlp1s0

3=hostname -I

Question:

What IP address did you get?
192.168.1.107 


part 3– Think Like an Analyst

Imagine:

Computer A:

192.168.1.10

Computer B:

192.168.1.50

Questions:

Are they likely on the same network?
Could they communicate directly?

Now another case:

Computer A:

192.168.1.10

Computer B:

8.8.8.8

Questions:

Which one is private?
Which one is public?
Would traffic to 8.8.8.8 normally go through your router?

Think before searching.
Answers

yes same network 
no router needed


2nd case
computer A is private 
computer b is public
if i need to communicate with this network then it will go through my router otherwise no 

