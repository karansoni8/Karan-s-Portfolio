# Karan Soni — SOC Analyst Portfolio

**Live site:** https://karansoni8.github.io/Karan-s-Portfolio/
**Resume:** [karan-soni-resume.pdf](karan-soni-resume.pdf)

Detection engineering portfolio for a blue-team analyst. Built around a
seven-host home SOC lab: what I detect, how the rules are tuned, and — deliberately —
where the coverage gaps are.

Oshawa, Ontario · open to hybrid and remote across Canada · available immediately.

---

## What's in the lab

| Role | Platform |
|---|---|
| SIEM | Elastic Stack — Elasticsearch, Kibana, Fleet |
| Endpoint telemetry | Sysmon + Elastic Agent |
| Network monitoring | Zeek 6.x |
| Perimeter | pfSense CE |
| Identity | Windows Server AD, AD Certificate Services, Group Policy |
| Offense | Kali Linux, Metasploit |
| Target | Metasploitable 2 |
| Second platform | Security Onion 2.4 (EVAL mode) |
| Also running | Splunk Universal Forwarder, Zabbix SNMP |

## Coverage

Eighteen MITRE ATT&CK techniques mapped across six tactics:

- **9 detections** written and tested against live attack traffic
- **6 techniques** with telemetry collected but rules not yet tuned
- **3 documented gaps** — T1204 user execution, T1558 Kerberos tickets, T1573 encrypted channel

The gaps are published on purpose. A coverage map with no gaps is a map nobody audited.

## Detections

Each of these was written, tuned against noise, then verified by running the
corresponding attack and confirming the rule fired.

| Technique | Detection | Data source |
|---|---|---|
| T1003.001 | LSASS handle access filtered on granted-access masks, not process name | Sysmon EID 10 |
| T1059.001 | Encoded PowerShell scoped by Office parent process | Sysmon EID 1 |
| T1071.001 | Beaconing by connection-interval variance (low jitter) | Zeek conn.log |
| T1210 | SMB exploitation attempt against a legacy host | Zeek notice |
| T1543.003 | Service installation on a domain controller | Windows Security 7045 |
| T1053.005 | Scheduled task creation outside a two-week baseline | Sysmon EID 1 + 4698 |
| T1110 | Failure-rate threshold per source with lockout correlation | Windows Security 4625 |
| T1136 | Account creation correlated to the creating session | Windows Security 4720 |
| T1190 | Exploitation of an internet-facing service | Zeek + pfSense |

## Incident walkthrough

One simulated intrusion followed end to end — macro execution, unalerted discovery,
credential access on the DC, lateral movement over SMB — with the triage call at each
stage and the rule changes that came out of it. Written up on the live site.

## Background

- Cybersecurity Graduate Certificate — Durham College, Oshawa, ON
- Diploma, Network Management with Cisco and Microsoft — LaSalle College, Montréal, QC
- Bachelor of Computer Applications — Parul University, India
- Cisco Networking Academy course certificate — CCNA: Enterprise Networking, Security
  and Automation, Jan 2025 *(Networking Academy curriculum certificate, not the
  Cisco 200-301 proctored exam — the 200-301 is in progress separately)*
- CompTIA CySA+ (CS0-004) — exam scheduled

## Contact

- sonikaran8899@gmail.com
- [linkedin.com/in/karan-soni-4b56a11b4](https://www.linkedin.com/in/karan-soni-4b56a11b4/)

---

## Repo contents

```
index.html               the portfolio site
karan-soni-resume.pdf    one-page resume
```

Static HTML, no build step, no dependencies. Served by GitHub Pages from `main`.
