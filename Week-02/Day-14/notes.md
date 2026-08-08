day 14

linux commands 

*ss=shows information about sockets and connections
*ss -t=shows tcp connections
*ss -u=shows udp connections
*ss -tuln=Show TCP and UDP ports that are currently listening, using numerical addresses/ports.
*ping -c 4 google.com=Sends 4 network requests to Google to check if it is reachable and how fast it responds.
*curl https://example.com=tells if web server is responding but in html(Give me the webpage),
*curl -I https://example.com=I asks for http header("Just tell me about the webpage response.").


— SOC Investigation

Imagine a user reports:

"My computer is communicating with an unknown external IP address."

You are investigating their Linux machine.

What would you check first?

Think about the commands you've learned.

Possible tools include:

ss
ps
ip a
ip route

Write your reasoning:
i will check from ss to know the ip and from whome its communicating then i will use ps to know more about process
