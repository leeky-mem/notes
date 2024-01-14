# Passive recon
## OSINT About products
- FCC ID https://fccid.io/
- Patents https://patents.google.com/
- Datasheets of components
- Social media, product forums, costumer reviews

## OSINT about companies
- Companie Homepage
- Social media, LinkedIn of employees
- Call them and ask.

## WHOIS
`whois` is a domain lookup tool.
It reveils usfull information about the domain and the domain registrar

### Usage
`whois DOMAIN` example `whois tryhackme.com`

## nslookup
Name Server Look Up: Used to look up Ip addresses, mail servers, text record and alike from a specific domain.

### Usage
`nslookup OPTIONS DOMAIN` example `nslookup -type=a tryhackme.com` to get type A records for the tryhackme.comm domain.

Options (`-type=`):
- A 	-> IPv4 Addresses
- AAAA 	-> IPv6 Addresses
- CNAME -> canonical name
- MX 	-> Mail Servers
- SOA 	-> Sart of Authority
- TXT 	-> Text records

## dig
dig is similar to nslookup. Sometime displays more info \
`dig DOMAIN OPTIONS` example: `dig tryhackme MX` to get the mailsercers of the tryhackme domain. Options: same as nslookup

## DNSDumpster (Webtool)
dnsdumpster.com
shows IPs, services, versions of services and OS

## Shodan (Webtool)
shodan.io
Shodan shows used IPs, ports, products, operating systems found of the target domain.

# Active recon
## Browser (Dev-tools and extensions)
The brower developer options reveal a ton of information about a target website.

### Extenstions
- FoxyProxy - lets you quickly change proxy-servers
- User-Agent Switcher and Manager - lets you change your user Agnets to pretend beeing a different browser or device
- Wappalyzer - shows technologies used on a particular website. Like: analytics, OS, Databases and so on.

## Traceroute
Used to determine how many hops you are away from the target 
`traceroute TARGET_IP`

## Telnet
Telnet is a programm which uses a protocol with the same name. Very old and mostly replaced by ssh.
It can be used though to connect to tcp ports and extract information like: banner, server versions etc.

### Usage
`telnet TARGET_IP PORT`

when prompted use `GET` requests to extract information. Like `GET /HTTP/1.1`

## Netcat
nc supports both TCP and UDP and can act as a clients and server.
It is a very versatlie tool and here are only the basics covered.

### Usage
`nc TARTGET_IP PORT` \
