# Karan Soni — SOC Analyst Portfolio

**[Live portfolio](https://karansoni8.github.io/Karan-s-Portfolio/)** · **[Résumé (PDF)](karan-soni-resume.pdf)** · **[LinkedIn](https://www.linkedin.com/in/karan-soni-4b56a11b4/)**

Detection engineering portfolio built around a seven-host home SOC lab: what I detect, how I tune the rules, and where the coverage gaps remain. An interactive attack walkthrough connects the activity on each host to the evidence an analyst sees and the decision that follows.

Oshawa, Ontario · open to hybrid and remote roles across Canada · available immediately.

## Explore the portfolio

- **Selected work:** four detection write-ups and one incident case study, with queries, tuning notes, and lessons learned.
- **ATT&CK coverage:** 18 mapped techniques, with selectable explanations of tested coverage, untuned telemetry, and known gaps.
- **Animated attack walkthrough:** five stages with moving evidence paths, highlighted hosts, play/pause, and manual stage navigation.
- **Microsoft Sentinel:** a detailed planned cloud lab, including its collection pipeline, proposed query, build plan, and validation checklist.
- **Experience and credentials:** IT support, security assessments, education, and linked course-completion badges.
- **Contact and résumé:** direct PDF access and a form that prepares an email draft.

The site uses a neutral charcoal palette, light/dark/system themes, responsive layouts, keyboard-accessible controls, and reduced-motion support.

## Home SOC lab

| Role | Platform |
| --- | --- |
| SIEM | Elastic Stack — Elasticsearch, Kibana, Fleet |
| Endpoint telemetry | Sysmon + Elastic Agent |
| Network monitoring | Zeek 6.x |
| Perimeter | pfSense CE |
| Identity | Windows Server AD, AD Certificate Services, Group Policy |
| Offense | Kali Linux, Metasploit |
| Target | Metasploitable 2 |
| Second platform | Security Onion 2.4 — EVAL mode |
| Also running | Splunk Universal Forwarder, Zabbix SNMP |

The expanded lab view includes the telemetry flow and the Linux endpoint blind spot: Zeek observed the SMB exploit traffic against Metasploitable, but the target had no endpoint agent.

## Coverage

Eighteen MITRE ATT&CK techniques mapped across six tactics:

- **9 detections** written and tested in the home lab.
- **6 techniques** with telemetry collected but rules not yet tuned.
- **3 documented gaps:** T1204 user execution, T1558 Kerberos tickets, and T1573 encrypted channel.

These counts describe the existing home lab. They do **not** include the planned Sentinel work.

The gaps are published on purpose. Collecting logs is not the same as detecting an attack.

## Detection work

The home-lab detections were developed and tuned using simulated attack activity. The site presents selected write-ups rather than nine separate rule pages.

| Technique | Detection | Data source |
| --- | --- | --- |
| T1003.001 | Suspicious LSASS handle access using granted-access masks and targeted exclusions | Sysmon EID 10 |
| T1059.001 | Encoded PowerShell scoped by parent process | Sysmon EID 1 |
| T1071.001 | Beaconing by connection-interval variance — low jitter | Zeek conn.log |
| T1210 | SMB exploitation attempt against a legacy host | Zeek notice |
| T1543.003 | Service installation on a domain controller | Windows Event 7045 |
| T1053.005 | Scheduled task creation outside a two-week baseline | Sysmon EID 1 + Windows Event 4698 |
| T1110 | Failure-rate threshold per source with lockout correlation | Windows Security Event 4625 |
| T1136 | Account creation correlated to the creating session | Windows Security Event 4720 |
| T1190 | Exploitation of a public-facing service in the lab | Zeek + pfSense |

The beaconing example on the site is labeled as illustrative detection logic, not a copy-and-run query.

## Animated incident walkthrough

One simulated intrusion, shown in the order it was investigated:

| Stage | What happens | Evidence and analyst decision |
| --- | --- | --- |
| 01 · Execution | An Office document launches encoded PowerShell | Sysmon EID 1; confirm the alert and recommend isolating the workstation |
| 02 · Discovery | The shell enumerates users and groups | Telemetry exists, but no tuned discovery rule fires; document the gap |
| 03 · Credential theft | LSASS access occurs on the domain controller | Sysmon EID 10; escalate and assess exposed credentials |
| 04 · Lateral movement | SMB admin-share access reaches a second host | Correlate network activity with credential theft; recommend containment and credential resets |
| 05 · Response | Review the incident and update the rules | Document changes and replay the scenario to verify improved coverage |

Use **Play walkthrough** for the narrated sequence, or select a stage to inspect it. The diagram distinguishes attacker activity, evidence sent to the SIEM, and telemetry without an alert. It is a visual simulation and does not control real systems.

## Microsoft Sentinel lab — planned

**Status: planned; implementation and validation are pending.** This section describes the lab I intend to build, not completed deployment or measured results.

### Proposed pipeline

**Windows security events → Azure Monitor Agent + data collection rule → Log Analytics → Sentinel analytics → incident investigation**

The proposed exercise starts with repeated failed Windows sign-ins, using Event 4625 as evidence. The example Kusto query groups failures by account, source IP, and five-minute window. Its threshold is a starting hypothesis that must be tested against normal traffic.

### Build and validation plan

1. Prepare an isolated Windows test environment, a Log Analytics workspace, and Microsoft Sentinel. Restrict administrative access and set collection/retention limits.
2. Configure Windows Security Events via AMA and a data collection rule. Verify event arrival, timestamps, and account/source fields.
3. Generate controlled failed sign-ins with test accounts, compare them with benign mistakes, and tune the query.
4. Configure a scheduled analytics rule, account/IP entity mapping, and incident creation. Review overlapping windows and alert grouping.
5. Investigate the resulting incident and publish sanitized evidence: connector health, sample events, query output, a timeline, and tuning notes.
6. Optionally add a Logic Apps playbook for enrichment or notification after the detection works. Keep containment a reviewed analyst decision.

The site includes an interactive pipeline, proposed query, and a checklist covering ordinary failed sign-ins, repeated failures, benign noise, and missing telemetry.

## Background

- Cybersecurity Graduate Certificate — Durham College, Oshawa, ON.
- Diploma, Network Management with Cisco and Microsoft — LaSalle College, Montréal, QC.
- Bachelor of Computer Applications — Parul University, India.
- Cisco Networking Academy course certificate — CCNA: Enterprise Networking, Security and Automation, January 2025. This is the curriculum certificate, not the Cisco 200-301 proctored exam; that exam is in progress separately.
- CompTIA CySA+ (CS0-004) — exam scheduled.

The portfolio links course-completion credentials from IBM SkillsBuild, Cisco Networking Academy, and AWS Academy. Course badges are distinguished from proctored certifications.

## Contact

- **Email:** [sonikaran8899@gmail.com](mailto:sonikaran8899@gmail.com)
- **LinkedIn:** [karan-soni-4b56a11b4](https://www.linkedin.com/in/karan-soni-4b56a11b4/)
- **Résumé:** [karan-soni-resume.pdf](karan-soni-resume.pdf)

The GitHub Pages contact form opens a prefilled draft in the visitor’s email application. The visitor must press **Send** there. The message stays on the page if an email application does not open.

Automatic form delivery is not enabled on the static site. A separate Node.js/Resend backend is available for deployment on a compatible host; it requires server-side email credentials.

## Repository contents

```text
index.html                 Portfolio, styles, scripts, and embedded images
karan-soni-resume.pdf       Résumé PDF
README.md                  Project overview
.nojekyll                  Static-site publishing marker
GITHUB-PAGES-SETUP.md       Upload and publishing instructions
```

The GitHub Pages version is static HTML with inline CSS and JavaScript: no build step and no runtime dependencies. Keep the résumé PDF beside `index.html`. The backend is a separate deployment and is not required to view this site.
