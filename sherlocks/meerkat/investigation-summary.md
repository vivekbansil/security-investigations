# Investigation Summary – Meerkat

## Scenario Overview
This investigation simulated a potential web application compromise. The objective was to analyze network traffic and security alerts to determine whether unauthorized access occurred, reconstruct the attacker’s activity timeline, and identify evidence of persistence.

## Artifacts Analyzed
- Packet capture (PCAP) data
- Suricata alert logs
- HTTP request and response activity
- Authentication patterns and command execution traces

## Analytical Process
The investigation began by reviewing Suricata alerts and correlating them with packet-level evidence in Wireshark to identify suspicious activity. Analysis of authentication patterns revealed abnormal login behavior consistent with credential abuse.

Further inspection of web traffic identified exploitation of a public-facing application vulnerability, enabling unauthorized functionality within the application. Subsequent network analysis revealed command execution behavior indicative of remote control activity.

Encrypted SSH traffic was observed following initial compromise. While payload contents were not directly visible due to encryption, upstream HTTP artifacts were analyzed to identify staging behavior consistent with persistence mechanisms.

Events were reconstructed chronologically to map the progression from initial access through post-exploitation activity.

## Findings
Correlated evidence confirmed that the host was successfully compromised via exploitation of a web application vulnerability after credential abuse. The attacker executed system-level commands and established persistence through modification of SSH authorized key files, enabling continued access.

Observed behaviors aligned with common adversary techniques involving valid account abuse, exploitation of public-facing applications, tool transfer, command execution, and SSH-based persistence.

## Lessons Learned
This investigation reinforced the importance of:
- Correlating IDS alerts with packet-level analysis
- Recognizing credential abuse patterns in authentication traffic
- Identifying web application exploitation indicators
- Understanding SSH key-based persistence mechanisms
- Reconstructing attack lifecycles from initial access through persistence
