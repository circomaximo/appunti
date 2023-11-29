Footprint and Reconaissance
DiR Busting and VHost enumeration

First of all install Wordlists if not already installed on our machine

sudo apt install seclists

now we can DIR BUSTING

GOBUSTER
gobuster dir -u http://10.10.10.10 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

FFUF
ffuf -u http://10.10.10.10/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

finding FILES
gobuster dir -u http://10.10.10.10 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .html,.css,.js

ffuf -u http://10.10.10.10/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -e .html,.css,.js,.conf


DNS ENUMERATION
dig zonetransfer.me
dig ns zonetransfer.me
dig mx zonetransfer.me

host zonetransfer.me
host -t ns zonetransfer.me
host -t cname zonetransfer.me

nslookup in windows
nslookup zonetransfer.me
nslookup
set type=ns
zonetransfer.me

ZONE TRANSFER  (identify the name server and initialize the zone transfer)\
host -t ns zonetransfer.me
host -l zonetransfer.me nsztm1.digi.ninja
dig axfr zonetransfer.me @nsztm1.digi.ninja

nslookup
> set type=ns
> zonetransfer.me
Server:  fritz.box
Address:  fd00::464e:6dff:fedc:436c

Risposta da un server non autorevole:
zonetransfer.me nameserver = nsztm1.digi.ninja
zonetransfer.me nameserver = nsztm2.digi.ninja
> server nsztm1.digi.ninja
Server predefinito:  nsztm1.digi.ninja
Address:  81.4.108.41
> set type=any
> zonetransfer.me
ls -d zonetransfer.me

dnsrecon -d zonetransfer.me -t axfr
dnsenum zonetransfer.me
fierce --domain zonetransfer.me

sudo apt install seclists
BRUTE FORCE DNS
sudo apt install seclists
nmap -p 53 --script dns-brute zonetransfer.me
dnsmap zonetransfer.me -w /usr/share/seclists/discovery/DNS/fierce-hotlists.txt
fierce --domain zonetransfer.me --subdomain-file /usr/share/seclists/discovery/DNS/fierce-hotlists.txt
