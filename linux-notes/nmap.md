# Host descovery
`nmap -sn <ip-range>` - The -sn options omits the portscan on newer versions of nmap you must be root to see the mac addresses.\
`-PR` - Only Arp scan, only works on the same subnet obviously i.e. same Ethernet, Wlan.\
`-PE` - ICMP echo request\
`-PP` - ICMP time stamp request\
`-PM` - ICMP address mask request\
TCP 3-way handshake: SYN | SYN,ACK | ACK\
`-PS<port-range-or-list>` - TCP syn scann (SYN | SYN,ACK | RST)\
`-PA<port>` - TCP ACK flag set (ACK | RST)\
`-PU` - UDP scan closed ports send back ICMP Type3 code3 back (Destination Unreachable)

Some reuests might be blocked by firewalls, therefore it is good to try different options for live host discovery.

# Port Scanning
Port Scan Type:\
`nmap -sT MACHINE_IP` - TCP Connect Scan \
`sudo nmap -sS MACHINE_IP` - TCP SYN Scan \
`sudo nmap -sU MACHINE_IP` - UDP Scan

## Options
`-p-` 					all ports\
`-p1-1023` 				scan ports 1 to 1023\
`-p443,8081,8080` list of ports\
`-F` 					100 most common ports\
`-r` 					scan ports in consecutive order\
`-T<0-5>` 				-T0 being the slowest and T5 the fastest\
`--max-rate 50` 		rate <= 50 packets/sec\
`--min-rate 15` 		rate >= 15 packets/sec\
`--min-parallelism 100` at least 100 probes in parallel

## Timings
nmap can be configured to waits a specific time between scanning two ports with the option `-T<0-5>`. The timings are:
- paranoid (0)
- sneaky (1)
- polite (2)
- normal (3) (default)
- aggressive (4)
- insane (5)

`-T0` waits 5 min between scans

in CTF often `-T4` is used for speed and in real life angagements `-T1` for stealth

## Advanced scanns
- Null scan `-sN`: No flags are set. An open port return nothing. A closed port returns RST/ACK

- FIN scan `-sF`: FIN flag is set. Again open port returns nothing, closed one returns RST/ACK

- Xmas scan `-sX`: FIN, PSH and URG flags are set. open port return nothing, closed port returns RST/ACK

For the scans above the ports are always labled open|filtered because the packets could be filtered by a firewall.

### Firewall scanning
- ACK scan `-sA`: ACK flag is set. If not blicked by firewall open and closed ports return RST. This scna is used to find ports not blocked by firewall.

- Window scan `-sW`: SImilar to ACK scan. inspects the window field of the answer. Also shows if a firewall is blocking port, but can give more information.

### Costum scan
- `--scanflags`: choos which flags are set. Example: `--scanflags RSTSYNFIN`

# Service Detection

A full connection is need for service detection. Can lead to discovery of the scan.

`nmap -sV TARGET_IP`

## Intensity levels
There are 10 intensity levels for the service scan. Level 0-9. \
`nmap -sV --version-intensitiy <0-9>` \
`--version-light` corresponds to level 2 \
`--version-all` corresponds to level 9 \

# OS Detection
nmap can detect the OS with fingerprinting and even guesses the kernel version. The kernel version detection is not that accurate though.

`-O` example with stealth scan: `nmap -sS -O TARGET_IP`

# nmap Scripting Engine (NSE)
scripts are located at `/usr/share/nmap/scripts`

The scripts can be very intrusive and often crash the system. So be carefull with them.

## Usage
`-sC` for default scripts example: `nmap -sS -sC TARGET_IP` \
`--script <script-name>` uses a specific script \
`--script <pattern*>` uses pattern and a wildcard to use all scripts in category. For example: `nmap -sS --script http*` 
