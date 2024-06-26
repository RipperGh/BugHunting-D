# WHOIS
We can consider WHOIS as the "white pages" for domain names.

It is a TCP-based transaction-oriented query/response protocol listening on TCP port 43 by default. We can use it for querying databases containing domain names, IP addresses, or autonomous systems and provide information services to Internet users. The protocol is defined in RFC 3912.

The first WHOIS directory was created in the early 1970s by Elizabeth Feinler and her team working out of Stanford University's Network Information Center (NIC). Together with her team, they created domains divided into categories based upon a computer's physical address. We can read more about the fascinating history of WHOIS here.

The WHOIS domain lookups allow us to retrieve information about the domain name of an already registered domain. The Internet Corporation of Assigned Names and Numbers (ICANN) requires that accredited registrars enter the holder's contact information, the domain's creation, and expiration dates, and other information in the Whois database immediately after registering a domain.

In simple terms, the Whois database is a searchable list of all domains currently registered worldwide.

WHOIS lookups were initially performed using command-line tools. Nowadays, many web-based tools exist, but command-line options often give us the most control over our queries and help filter and sort the resultant output.

Sysinternals WHOIS for Windows or Linux WHOIS command-line utility are our preferred tools for gathering information. However, there are some online versions like whois.domaintools.com we can also use.

We would get the following response from the previous command to run a whois lookup against the facebook.com domain. An example of this whois command is:
```
GhostRipper@htb[/htb]$ export TARGET="facebook.com" # Assign our target to an environment variable
GhostRipper@htb[/htb]$ whois $TARGET

Domain Name: FACEBOOK.COM
Registry Domain ID: 2320948_DOMAIN_COM-VRSN
Registrar WHOIS Server: whois.registrarsafe.com
Registrar URL: https://www.registrarsafe.com
Updated Date: 2021-09-22T19:33:41Z
Creation Date: 1997-03-29T05:00:00Z
Registrar Registration Expiration Date: 2030-03-30T04:00:00Z
Registrar: RegistrarSafe, LLC
Registrar IANA ID: 3237
Registrar Abuse Contact Email: abusecomplaints@registrarsafe.com
Registrar Abuse Contact Phone: +1.6503087004
Domain Status: clientDeleteProhibited https://www.icann.org/epp#clientDeleteProhibited
Domain Status: clientTransferProhibited https://www.icann.org/epp#clientTransferProhibited
Domain Status: clientUpdateProhibited https://www.icann.org/epp#clientUpdateProhibited
Domain Status: serverDeleteProhibited https://www.icann.org/epp#serverDeleteProhibited
Domain Status: serverTransferProhibited https://www.icann.org/epp#serverTransferProhibited
Domain Status: serverUpdateProhibited https://www.icann.org/epp#serverUpdateProhibited
Registry Registrant ID:
Registrant Name: Domain Admin
Registrant Organization: Facebook, Inc.
Registrant Street: 1601 Willow Rd
Registrant City: Menlo Park
Registrant State/Province: CA
Registrant Postal Code: 94025
Registrant Country: US
Registrant Phone: +1.6505434800
Registrant Phone Ext:
Registrant Fax: +1.6505434800
Registrant Fax Ext:
Registrant Email: domain@fb.com
Registry Admin ID:
Admin Name: Domain Admin
Admin Organization: Facebook, Inc.
Admin Street: 1601 Willow Rd
Admin City: Menlo Park
Admin State/Province: CA
Admin Postal Code: 94025
Admin Country: US
Admin Phone: +1.6505434800
Admin Phone Ext:
Admin Fax: +1.6505434800
Admin Fax Ext:
Admin Email: domain@fb.com
Registry Tech ID:
Tech Name: Domain Admin
Tech Organization: Facebook, Inc.
Tech Street: 1601 Willow Rd
Tech City: Menlo Park
Tech State/Province: CA
Tech Postal Code: 94025
Tech Country: US
Tech Phone: +1.6505434800
Tech Phone Ext:
Tech Fax: +1.6505434800
Tech Fax Ext:
Tech Email: domain@fb.com
Name Server: C.NS.FACEBOOK.COM
Name Server: B.NS.FACEBOOK.COM
Name Server: A.NS.FACEBOOK.COM
Name Server: D.NS.FACEBOOK.COM
DNSSEC: unsigned

<SNIP>
```
We can gather the same data using whois.exe from Windows Sysinternals:
```
C:\htb> whois.exe facebook.com

Whois v1.21 - Domain information lookup
Copyright (C) 2005-2019 Mark Russinovich
Sysinternals - www.sysinternals.com

Connecting to COM.whois-servers.net...

WHOIS Server: whois.registrarsafe.com
   Registrar URL: http://www.registrarsafe.com
   Updated Date: 2021-09-22T19:33:41Z
   Creation Date: 1997-03-29T05:00:00Z
   Registry Expiry Date: 2030-03-30T04:00:00Z
   Registrar: RegistrarSafe, LLC
   Registrar IANA ID: 3237
   Registrar Abuse Contact Email: abusecomplaints@registrarsafe.com
   Registrar Abuse Contact Phone: +1-650-308-7004
   Domain Status: clientDeleteProhibited https://icann.org/epp#clientDeleteProhibited
   Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
   Domain Status: clientUpdateProhibited https://icann.org/epp#clientUpdateProhibited
   Domain Status: serverDeleteProhibited https://icann.org/epp#serverDeleteProhibited
   Domain Status: serverTransferProhibited https://icann.org/epp#serverTransferProhibited
   Domain Status: serverUpdateProhibited https://icann.org/epp#serverUpdateProhibited
   Name Server: A.NS.FACEBOOK.COM
   Name Server: B.NS.FACEBOOK.COM
   Name Server: C.NS.FACEBOOK.COM
   Name Server: D.NS.FACEBOOK.COM
   DNSSEC: unsigned
   URL of the ICANN Whois Inaccuracy Complaint Form: https://www.icann.org/wicf/
>>> Last update of whois database: 2021-10-11T06:03:10Z <<<

<SNIP>
```
From this output, we have gathered the following information:
  - Organisation: Facebook, Inc.
  - Locations	US, 94025 Menlo Park, CA, 1601 Willo Rd
  - Domain Email address	domain@fb.com
  - Registrar Email address	abusecomplaints@registrarsafe.com
  - Phone number	+1.6505434800
  - Language	English (US)
  - Registrar	RegistrarSafe, LLC
  - New Domain	fb.com
  - DNSSEC	unsigned
  - Name servers
    - A.NS.FACEBOOK.COM
    - B.NS.FACEBOOK.COM
    - C.NS.FACEBOOK.COM
    - D.NS.FACEBOOK.COM

# Exercise 
1) Question: Perform a WHOIS lookup against the paypal.com domain. What is the registrar Internet Assigned Numbers Authority (IANA) ID number?

Answer: 292

2) Question: What is the admin email contact for the tesla.com domain (also in-scope for the Tesla bug bounty program)?

Answer: admin@dnstinations.com

How I go the answer:
GhostRipper@htb[/htb]$ export TARGET="target.com" # Assign our target to an environment variable
GhostRipper@htb[/htb]$ whois $TARGET


