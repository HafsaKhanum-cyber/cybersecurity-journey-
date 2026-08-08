day 11

part 1=theory

SSL =ssl was used before to encrpt traffic for secure communication 
& 
TLS=tls is now used by websites to encrpt communication better version of ssl
digital certificates=that verifies the website is authentic
public & private keys=used for encryption
certificate authority(CA)=the authority which issues certificates of website


part 2=practical

1=Run:
openssl s_client -connect google.com:443


 Questions

1.  Which TLS version do you see? 

Answer:TLSv1.3

2. Who issued the certificate? 

Answer:google trust services

3.  Which website did the certificate belong to? 

Answer:google.com


2=Open:

https://google.com

Click the 🔒 padlock icon.

View the certificate.

Look for:

Valid From=Monday, July 20, 2026 at 11:05:56 PM
Valid To=Monday, October 12, 2026 at 11:05:55 PM
Issued By=Google Trust Services (WR2)

part 3=SOC Investigation 

A user reports:

"I received an email saying my account will be permanently locked unless I click a link and verify my password."

Questions
1. What could cause this?

obviosly a fake email phsishing

2. Would you click the link?

no because its definately fake no companies ask for personal details like these

3. What would you investigate first?

where the link and email came from

4. What evidence would you look for to decide whether the email is legitimate or phishing?

will check if the url belongs to company and the sender information 



