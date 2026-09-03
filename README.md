# Network Intrusion Analysis Capstone (CodePath CYB102)

Team capstone for CodePath's CYB102 cybersecurity course, Summer 2026. We analyzed the
CICIDS2017 network intrusion dataset, adapted a CERT incident-response playbook to the attack
traffic it contains, and presented our findings at Demo Day.

**Slides:** [Final presentation (Google Slides)](https://docs.google.com/presentation/d/1gba2BeBFWIFMluYRmWvGFd2_8iWJ-T5h-JiCsGcFps0/view) | [PDF copy](./CYB102-CICIDS2017-slides.pdf)

## What we did

CICIDS2017 is a labeled network traffic dataset from the Canadian Institute for Cybersecurity
that mixes benign traffic with common attacks (DDoS, DoS, brute force, port scans, web attacks,
botnet, infiltration). We treated it as if it were traffic from a real organization and worked
through the incident lifecycle:

1. **Preparation.** Selected the dataset, defined scope, and chose the CERT Société Générale
   IRM-4 (DDoS) incident response playbook as our baseline, with CISA and NIST guidance as
   references. We then customized the playbook for the attack patterns present in CICIDS2017
   rather than using it as-is.
2. **Detection and analysis.** Loaded the CICFlowMeter CSVs into Splunk and tested three
   hypotheses about the attack traffic: (1) malicious traffic volume significantly exceeds
   benign traffic, (2) attacks target only a few systems or services, and (3) attack activity
   occurs in predictable time windows.
3. **Tooling.** Evaluated and documented the tools an analyst would use on this traffic:
   tcpdump, Wireshark/Tshark, Snort, NetFlow, and Ntop, with notes on what each is good for at
   which stage of the investigation.
4. **Impact analysis and triage.** Assessed the business impact of the observed attacks and
   defined how incidents would be triaged and tracked in a case management system.
5. **Threat intelligence.** Mapped observed activity to external threat intel sources and
   indicators.
6. **Presentation.** A 7 to 10 minute Demo Day presentation covering the above.

## Key findings

- **One host absorbed almost everything.** The web server (192.168.10.50) received 555,630 of
  557,646 malicious events (99.6%). By volume: Hulk DoS (231,073, port 80), PortScan (158,930,
  many ports), DDoS (128,024, port 80), FTP-Patator (7,937, port 21), SSH-Patator (5,897, port 22).
- **All three hypotheses were only partially true.** Volume-based detection catches Hulk and
  FTP-Patator but misses low-rate attacks like Slowloris; attacks concentrated on one host but
  spread across many services on it (roughly 1,000 ports probed on a single IP); scheduled
  attacks fell in predictable windows, but botnet C2 traffic ran as prolonged low-level activity
  outside them.
- **Two Splunk queries drove the investigation:** one grouping malicious events by destination
  asset, one linking the web server to specific attack labels and service ports, so analysis
  targeted the affected host instead of searching blindly.
- **Remediation was mapped per attack class:** rate limiting, lockouts, and key-based SSH for
  brute force; upstream protection, connection limits, and volume alerts for DoS/DDoS; closing
  unused ports, firewall rules, and segmentation for scans; endpoint isolation and C2/DNS
  monitoring for botnet activity.

## Repository contents

|| File | Description |
|------|-------------|
| `CYB102-CICIDS2017-slides.pdf` | Final Demo Day presentation (16 slides) |

## Team and my role

Five-person team: Markian Zabihaylo, Xiaoming Wang, Jacob Trudeau, Sahra Mizuguchi, and
Shaquale Carmichael.

My contributions:

- Wrote the **tooling section**: evaluated tcpdump, Wireshark/Tshark, Snort, NetFlow, and Ntop
  and documented how each fits into detection and investigation of the CICIDS2017 attacks.
- Co-authored the **impact analysis** and the **triage and case management** sections with
  Jacob Trudeau.
- Presented at Demo Day.

## Dataset

Sharafaldin, I., Lashkari, A. H., and Ghorbani, A. A. "Toward Generating a New Intrusion
Detection Dataset and Intrusion Traffic Characterization." ICISSP 2018.
Dataset: https://www.unb.ca/cic/datasets/ids-2017.html

The dataset itself is not included in this repository.
