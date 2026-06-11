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



## Splunk Security Event Monitoring Lab

Windows Security Event Logs were ingested into Splunk Enterprise to simulate SOC-style monitoring and authentication event analysis workflows.

### Log Sources
- Windows Security Event Logs
- Windows System Logs
- Windows Application Logs

### Splunk Searches Performed

#### Failed Login Detection
```spl
source="WinEventLog:Security" EventCode=4625
```
Observed failed Windows authentication attempts generated intentionally during lab testing.

![Failed Login Detection](screenshots/splunk-failed-login-detection.png)

Observed successful Windows authentication events.

![Successful Login Detection](screenshots/splunk-successful-login-detection.png)

#### Process Creation Monitoring
```spl
source="WinEventLog:Security" EventCode=4688
```

Used to identify process execution activity within the Windows environment.

![Process Monitoring](screenshots/splunk-process-monitoring.png)

### Security Assessment

Splunk successfully ingested and indexed Windows event logs, allowing detection and investigation of authentication-related security events. Simulated failed login activity was successfully identified using Splunk search queries.


Sysmon Endpoint Monitoring

Project Objective

The objective of this phase of the home lab was to deploy Sysmon on a Windows host and integrate Sysmon telemetry into Splunk Enterprise for enhanced endpoint visibility and security monitoring.

Tools Used
Sysmon
Splunk Enterprise
Splunk Universal Forwarder
Windows Event Viewer
Windows Command Prompt
Lab Configuration

A Windows endpoint was configured with Sysmon to generate detailed endpoint telemetry, including process creation activity. Splunk Universal Forwarder was configured to collect Sysmon Operational logs and forward them to Splunk Enterprise for centralized analysis.

Deployment Steps
Sysmon Installation

Sysmon was installed on the Windows host using a custom XML configuration file.

Log Verification

Sysmon Operational logs were verified within:

Applications and Services Logs
└── Microsoft
    └── Windows
        └── Sysmon
            └── Operational

Event ID 1 (Process Creation) events were successfully generated and observed.

Splunk Forwarding Configuration

The Splunk Universal Forwarder was configured to collect:

Microsoft-Windows-Sysmon/Operational

and forward events to Splunk Enterprise for indexing and analysis.

Troubleshooting and Investigation

During deployment, Sysmon events were not initially appearing within Splunk despite being visible in Windows Event Viewer.

Investigation Process

The following troubleshooting steps were performed:

Verified Sysmon Operational logging was enabled
Confirmed Event ID 1 events existed within Event Viewer
Verified Universal Forwarder connectivity to Splunk
Reviewed Splunk Universal Forwarder log files
Identified repeated subscription failures for the Sysmon event channel

Error observed:

Could not subscribe to Windows Event Log channel
Microsoft-Windows-Sysmon/Operational

errorCode=5
Root Cause

The Splunk Universal Forwarder service account did not have sufficient permissions to subscribe to the Sysmon Operational event channel.

Resolution

The Universal Forwarder service was reconfigured to run under:

Local System

After restarting the service, Sysmon events were successfully collected and forwarded to Splunk.

Validation

Successful ingestion of Sysmon telemetry was confirmed using the following Splunk search:

source="WinEventLog:Microsoft-Windows-Sysmon/Operational"

Results confirmed:

Successful log ingestion
Process Creation telemetry collection
Continuous endpoint activity monitoring
Thousands of indexed Sysmon events

Security Analysis

Sysmon provides enhanced endpoint visibility beyond standard Windows Event Logs.

Observed telemetry included:

Process creation activity
Parent-child process relationships
Command-line execution details
User context information
Application execution tracking

This telemetry improves detection capabilities for suspicious process execution and endpoint-based threats.





## Security Notes
 Sensitive internal network information and identifiers were sanitized before publication.








