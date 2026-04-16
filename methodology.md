# Investigation Methodology

Across all investigations, the following general approach was applied:

1. **Initial signal review to understand scope and environment**
Start by understanding what is being asked and identifying the systems involved (e.g., public-facing servers, internal hosts, domain controllers). This includes getting familiar with available data sources such as PCAPs, event logs, and provided artifacts.
2. **Identification and prioritization of relevant artifacts**
Determine which data sources are most useful for the current question or stage of the investigation (network traffic, Windows event logs, web server activity, etc.). Focus on narrowing down noise and isolating meaningful signals.
3. **Hypothesis-driven analysis**
Form simple working hypotheses (e.g., initial access via web app, possible lateral movement, command execution) and test them against the data. Adjust direction as new evidence is uncovered rather than searching blindly.
4. **Deep inspection of evidence (logs, traffic, and content)**
Analyze artifacts at a granular level:

Follow HTTP streams in PCAPs
Parse and filter logs using command-line tools (grep, jq)
Inspect file contents and scripts when available
This step often includes pivoting from high-level indicators to raw data for confirmation.
5. **Correlation across multiple data sources**
Link activity between systems and data types (e.g., mapping network traffic to host-level actions or connecting a downloaded script to later behavior). This helps reconstruct attacker movement across the environment.
6. **Understanding attacker behavior and tooling**
When needed, pivot to external resources (e.g., GitHub, public write-ups) to better understand unfamiliar techniques such as web shells or tunneling mechanisms. Focus on identifying how the tool works rather than memorizing it.
7. **Reconstruction of the attack chain**
Build a clear timeline of events from initial access to later stages (execution, lateral movement, persistence). This helps answer questions accurately and reinforces understanding of the full incident.
8. **Final assessment and validation**
Confirm findings with direct evidence (not assumptions), ensuring answers are supported by logs, traffic, or code. Re-check conclusions for accuracy before finalizing.
9. **Documentation of findings and lessons learned**
Summarize the investigation in a structured way, focusing on what happened, how it was identified, and what was learned. This reinforces understanding and builds a reusable knowledge base.

---

This methodology reflects practical SOC-style investigation: starting broad, narrowing focus, validating with evidence, and tying everything back to attacker behavior.
