# cybersecurity home-lab
 Project Overview
This project simulates a basic Security Operations Center (SOC) traffic analysis investigation using Wireshark in a virtualized lab environment. The objective was to capture and analyze network traffic, including ICMP, DNS, TCP, and HTTPS communications, to better understand normal network behavior and foundational security analysis workflows.

## Tools Used
- Wireshark
- Ubuntu Linux Virtual Machine
- Oracle VirtualBox
- Linux networking utilities (`ping`, `curl`, `nslookup`)

- Lab Environment
A controlled virtual lab environment was configured using Ubuntu Linux running inside Oracle VirtualBox. Network traffic was intentionally generated and captured for analysis using Wireshark.

## Traffic generated included:
- ICMP ping requests
- DNS lookups
- HTTPS web traffic
- TCP connections

## Traffic Analysis
  -ICMP Analysis
 ICMP Echo Requests and Echo Replies were analyzed to observe connectivity testing behavior between the internal virtual machine and external hosts.
## Observations
- Successful ICMP request/reply communication observed
- Consistent TTL values identified
- No signs of packet flooding or suspicious scanning behavior
## Security Assessment
 The observed ICMP traffic appeared to be legitimate diagnostic traffic commonly associated with standard network connectivity testing.

## Key Learnings
- Learned how to capture and inspect network packets using Wireshark
- Analyzed ICMP request and reply behavior
- Observed normal network communication patterns
- Practiced SOC-style traffic investigation and documentation
- Improved understanding of packet-level analysis workflows

##  HTTPS / TLS Traffic Analysis
Encrypted HTTPS traffic was analyzed to observe secure client-server communication and TLS session establishment behavior.
### Observations
- Multiple outbound TCP connections observed over port 443
- TLSv1.2 encrypted sessions identified
- TLS handshake activity captured, including:
  - Client Key Exchange
  - Change Cipher Spec
  - Encrypted Handshake Messages
- Encrypted application data successfully transmitted between client and remote host

### Security Assessment
The observed traffic appeared consistent with legitimate encrypted HTTPS browsing activity. No suspicious or anomalous encrypted traffic patterns were identified during analysis.

## TCP Handshake Analysis
TCP connection establishment behavior was analyzed using Wireshark to observe the standard TCP three-way handshake process and session termination activity.

### Observations
- TCP SYN/ACK packets observed during HTTPS session establishment
- ACK packets confirmed successful client-server communication
- FIN/ACK packets identified during graceful TCP session termination
- Multiple outbound TCP connections established over port 443

  ### Security Assessment
Observed TCP behavior appeared consistent with legitimate encrypted web traffic and standard client-server communication patterns. No suspicious or malformed TCP activity was identified during analysis.

## 📷 TCP Packet Capture

![TCP Analysis](screenshots/tcp-handshake-analysis.png)



##  DNS Traffic Analysis
DNS traffic was analyzed to observe hostname resolution behavior and DNS query activity generated within the Ubuntu virtual machine environment.

### Observations
- Standard DNS queries and responses successfully captured
- Both A (IPv4) and AAAA (IPv6) record lookups were identified
- DNS communication observed between the local resolver and the external DNS server
- Successful domain resolution confirmed for reddit.com

### Security Assessment
Observed DNS activity appeared consistent with legitimate user-generated browsing traffic and standard hostname resolution behavior. No suspicious or malicious domain requests were identified during analysis.

## 📷 DNS Packet Capture

![DNS Analysis](screenshots/dns-analysis.png)



## Security Notes
 Sensitive internal network information and identifiers were sanitized before publication.








