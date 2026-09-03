# Network Intrusion Analysis Capstone (CodePath CYB102)

Team capstone for CodePath's CYB102 cybersecurity course, Summer 2026. We analyzed the
CICIDS2017 network intrusion dataset, adapted a CERT incident-response playbook to the attack
traffic it contains, and presented our findings at Demo Day.

**Slides:** [Final presentation (PDF)](./slides.pdf)

## What we did

CICIDS2017 is a labeled network traffic dataset from the Canadian Institute for Cybersecurity
that mixes benign traffic with common attacks (DDoS, DoS, brute force, port scans, web attacks,
botnet, infiltration). We treated it as if it were traffic from a real organization and worked
through the incident lifecycle:

1. **Preparation.** Selected the dataset, defined scope, and chose the CERT Société Générale
   IRM-4 (DDoS) incident response playbook as our baseline. We then customized the playbook for
   the attack patterns present in CICIDS2017 rather than using it as-is.
2. **Detection and analysis.** Loaded the flow-level CSVs into Splunk and tested three
   hypotheses about the attack traffic: [HYPOTHESIS 1], [HYPOTHESIS 2], [HYPOTHESIS 3].
3. **Tooling.** Evaluated and documented the tools an analyst would use on this traffic:
   tcpdump, Wireshark/Tshark, Snort, NetFlow, and Ntop, with notes on what each is good for at
   which stage of the investigation.
4. **Impact analysis and triage.** Assessed the business impact of the observed attacks and
   defined how incidents would be triaged and tracked in a case management system.
5. **Threat intelligence.** Mapped observed activity to external threat intel sources and
   indicators.
6. **Presentation.** A 7 to 10 minute Demo Day presentation covering the above.

## Key findings

- [FINDING 1: e.g. which attack class dominated the dataset and how it showed up in Splunk]
- [FINDING 2: e.g. which hypothesis was confirmed or rejected, and by what evidence]
- [FINDING 3: e.g. a detection gap in the original playbook that the customized version closes]

## Repository contents

| File | Description |
|------|-------------|
| `slides.pdf` | Final Demo Day presentation |
| `playbook.md` | CERT IRM-4 DDoS playbook, customized for CICIDS2017 |
| `tools.md` | Tooling evaluation: tcpdump, Wireshark/Tshark, Snort, NetFlow, Ntop |
| `impact-and-triage.md` | Impact analysis and triage / case management design |

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
