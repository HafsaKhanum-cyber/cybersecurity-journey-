day 10 

HTTP & HTTPS Fundamentals

PART 1=theory

What is HTTP?

HTTP (HyperText Transfer Protocol) is the protocol used to transfer  web content between a browser and a web server.

HTTP Request=An HTTP Request is sent by the client (browser) to the server.

It asks for something.

Example:

GET / HTTP/1.1
Host: example.com

This means:
"Please send me the homepage."

HTTP Response=The server replies with an HTTP Response.

Example:

HTTP/1.1 200 OK

Meaning:

"Everything worked. Here's the page."

HTTP Methods:
1=GET=gets information from the server
2=POST=Sends data to the server.
3=PUT=Updates existing information.
4=DELETE=Deletes information.
5=PATCH=Updates part of existing data.

HTTP Status Codes
1=200 OK=Everything worked.
2=301 Moved Permanently=The page has moved to another location.
3=403 Forbidden=You are not allowed to access the page.
4=404 Not Found=The page doesn't exist.
5=500 Internal Server Error=Something went wrong on the server.

HTTP vs HTTPS
HTTP	       HTTPS
No encryption, Encrypted
Port 80,       Port 443
Data can be 
read if 
intercepted,   Data is encrypted using TLS
Less secure,   More secure


Part 2– Practical Lab

Browser Developer Tools

Open Google Chrome or Firefox.

Press:

F12

or

Ctrl + Shift + I

Go to the Network tab.

Now visit:

https://example.com


Refresh the page.

Questions
What is the first request?

Answer: 
example.com because i requested this one

Which HTTP method is used?

Answer:get

What status code do you see?

Answer:304

Is the connection HTTP or HTTPS?

Answer:https

--Wireshark Connection

Open Wireshark.

Capture traffic.

Visit:

https://example.com

Questions:

Can you still read the webpage contents?

Why or why not?

Answer:No, I cannot read the webpage contents because the connection uses HTTPS. HTTPS encrypts the data using TLS, so Wireshark can capture the packets but cannot read the actual webpage content.

Part 3 – SOC Investigation

A user reports:

"I keep getting a 404 Not Found error."

Questions
What does 404 mean? 
page doesnot exists 

Is this usually a network problem? 
no it is not the page doesnot exist 

What would you investigate first?
Verify the URL is correct.
Check if the page/resource has been moved or deleted.
Look for broken links.


