GitHub README Format - Active Directory + Splunk SOC Homelab
# Active Directory + Splunk SOC Homelab

This project is a beginner SOC analyst homelab built in VMware Workstation. The goal was to create a small business-style Windows domain environment and connect it to Splunk so Windows security logs could be collected, searched, and used for basic detections.
## Project Overview

I built a virtual cybersecurity lab using Windows Server 2022, Windows 10 Pro, Splunk Enterprise, and Splunk Universal Forwarder. The lab includes a domain controller, a domain-joined Windows client, and a dedicated Splunk server used as a basic SIEM. This project helped me practice Active Directory administration, Windows networking, log forwarding, Splunk searching, and basic SOC alert creation.
## Lab Environment

- DC01 — Windows Server 2022 Domain Controller
- CLIENT01 — Windows 10 Pro Workstation
- SPLUNK01 — Splunk Enterprise SIEM Server

All virtual machines were connected through VMware NAT networking and configured with static IP addresses.
## Network Layout

```text
DC01      192.168.100.10
CLIENT01  192.168.100.20
SPLUNK01  192.168.100.30
Gateway   192.168.100.2
```
## What I Built

- Configured Windows Server 2022 Active Directory Domain Services
- Created and managed the `homelab.local` domain
- Joined Windows 10 workstation to the domain
- Installed Splunk Enterprise on SPLUNK01
- Installed Splunk Universal Forwarder on DC01 and CLIENT01
- Configured centralized Windows Event Log collection
- Troubleshot VMware networking and DNS issues
- Created beginner SOC detections and alerts
## Splunk Forwarder Configuration

### outputs.conf

```ini
[tcpout]
defaultGroup = default-autolb-group

[tcpout:default-autolb-group]
server = 192.168.100.30:9997
```

### inputs.conf

```ini
[WinEventLog://Security]
disabled = 0

[WinEventLog://System]
disabled = 0

[WinEventLog://Application]
disabled = 0
```
## Logs Collected

- Security Logs
- System Logs
- Application Logs
- Login Activity
- Failed Login Attempts
- User Account Creation Events
## Splunk Searches Used

```spl
index=*
```

```spl
index=* EventCode=4624
```

```spl
index=* EventCode=4625
```

```spl
index=* EventCode=4720
```

```spl
index=* | stats count by host
```
## SOC Alerts Built

- Failed Login Detection
- Successful Login Detection
- New User Account Creation Detection
- Account Lockout Detection
- Group Membership Change Detection
## Problems Troubleshot

- VMware NAT networking issues
- DNS resolution failures
- Splunk Universal Forwarder inactive status
- Windows Firewall communication issues
- Incorrect `inputs.conf.txt` file extension
- Static IP addressing problems
- No internet connectivity inside VMs
## Skills Practiced

- VMware Workstation
- Windows Server 2022 Administration
- Active Directory
- Windows Networking
- DNS Troubleshooting
- Splunk Enterprise
- Splunk Universal Forwarder
- Windows Event Log Collection
- SPL Searching
- Beginner SOC Alerting
## Resume Description

Built a virtual SOC homelab using VMware, Windows Server 2022, Windows 10 Pro, Active Directory, Splunk Enterprise, and Splunk Universal Forwarder. Configured a domain controller and domain-joined workstation, centralized Windows event logs into Splunk, troubleshot networking and forwarding issues, and created beginner SOC detections for login activity and account changes.
