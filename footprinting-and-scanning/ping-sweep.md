---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Ping sweep

## Nmap

```bash
# Scan IP Subnets
sudo nmap -sn -oN output.txt $IP/24 | grep for | cut -d" " -f5

# Scan IP List File
sudo nmap -sn -iL iplist.txt -oN output.txt | grep for | cut -d" " -f5

# Scan IP Range Octet
sudo nmap -sn -oN output.txt $IP-20 | grep for | cut -d" " -f5

# Trace ARP/ICMP Reply
sudo nmap -sn -oN output.txt $IP -PE --packet-trace

# Show the reason target marked "alive"
sudo nmap -sn -oN output.txt $IP -PE --reason

# Only ICMP without Arp Ping
sudo nmap -sn -oN output.txt $IP -PE --packet-trace --disable-arp-ping
```

## General Ping

```bash
# Standard ping
ping -c 1 $IP

# Entire subnets
fping -I eth0 -g $IP/24 -a 2>/dev/null

# Get the IP and MAC address
sudo arp-scan -I eth0 -g $IP/24
```
