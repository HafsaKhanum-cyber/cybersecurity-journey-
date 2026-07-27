day 5

part 1=DNS 

why dns exists =
to convert domain name to ip addresses

how dns works=
client type google.com 1st browser asks computer if the ip address exits the website load otherwise the browser goes to dns resolver which acts as a manager of dns and resolver goes to root dns server and asks about google.com then root server acts as a guide and tells about .com server and redirects the resolver to .com server then .com server redirects to google server and it provides  ip address to the dns resolver and it gives to browser and website loads

Dns cache=
stores already used ip addresses to avoid long process again and again 

Dns record types=some common types

A record :domain to ip adress(for ipv4)
AAAA record:same as A record but for IPV6
MX record:mail exchange 
Cname record:two alike names but both have 1 ip address 
NS record:name server 
TXT record:text information


PART 2=linux practical
*Run:

nslookup google.com

Questions:

Which IP address did you get?
Which DNS server answered?

server:		127.0.0.53
Address:	127.0.0.53#53

Non-authoritative answer:
Name:	google.com
Address: 142.250.202.238
Name:	google.com
Address: 2a00:1450:4018:810::200e


*Run:

nslookup github.com

Questions:

Is the IP different from Google's?
Why?

Answers;

yes the ip is different from google.com

because both are different domain names and each domain is assigned with unique ip address 

*Run

dig google.com 

it told about which dns record it returned my retured A record 

ANSWER SECTION:
google.com.		46	IN	A	142.250.186.14


part 3=dns and cybersecurity

attacks 
1=dns spoofing:redirects to fake wedsite 
2=dns tunneling:hides data in dns requests to bypass security tests
3=dns cache poisoning:hides data in dns cache

part 4=the SOC scenario:

A user says, "Google isn't opening." What are at least 5 possible causes before you conclude that Google is down?

ANSWER=

1=dns not responding 
2=browser issue
3=internet connection issue
4=https blocked on computer
5=firewall restrictions 

