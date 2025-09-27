# Project 1: Log Analysis & SIEM Simulations
**Skills: Threat detection, log correlation, SIEM workflows.**
  -  Deploy Zeek and Suricata on a SPAN/mirror port in your homelab.
  -  Forward logs into Elastic Stack (ELK) (completely free, open source).
  -  Build dashboards for DNS tunneling, brute force, and phishing attempts.
  -  Add MITRE ATT&CK mapping annotations to detections.
  -  Apply NIST 800-53 AU-6 (audit review) and SI-4 (system monitoring) compliance language in documentation.

✅ Covers: CySA+ Domain 1 (Threat Management) + CSSP Analyst requirement (log analysis / SIEM triage).


# Project 2: SOC Analyst Playbook
***Skills: Incident response, governance, compliance.****
  - Build IR playbooks in Markdown/YAML (versioned in GitHub).
  - Align playbooks with NIST 800-61 IR lifecycle (Prep → Detect → Contain → Eradicate → Recover → Lessons Learned).
  - Automate IOC lookups with Python + VirusTotal Public API (free).
  - Document authority boundaries (who authorizes containment actions).
  - Add chain-of-custody steps for evidence preservation.

✅ Covers: CySA+ Domain 4 (Incident Response) + CSSP Incident Responder requirement (IR procedures, escalation).


# Project 3: Detection Engineering with Sigma & YARA
***Skills: Custom detections, detection validation.***
  - Write Sigma rules for Sysmon logs (Windows endpoint).
  - Write YARA rules to catch macro malware and LOLBins.
  - Test rules with Atomic Red Team payloads (free).
  -  Automate YARA scans with a Python script, forwarding results into ELK.
  -  Document rule change management (approvals, versioning) for compliance with NIST CM-3 (configuration management).

✅ Covers: CySA+ Domain 2 (Software & System Security / Threat Detection Engineering) + CSSP Analyst requirement (creating and tuning detections).


# Project 4 (New): Vulnerability Management & Risk Mitigation
***Skills: Vulnerability scanning, risk assessment, remediation planning.***
  -  Run OpenVAS/Greenbone Community Edition (completely free) inside your homelab.
  -  Scan a test machine (Windows 10 VM + Ubuntu VM) for missing patches and misconfigurations.
  -  Export findings to CSV/JSON and prioritize by CVSS score.
  -  Document mitigations in a risk register (Markdown table in GitHub).
  -  Map results to NIST 800-53 RA-5 (vulnerability scanning) and CIS Control 7 (continuous vulnerability management).
  -  Add remediation tracking → demonstrate documenting patch cycles and assigning responsibilities (simulated).

✅ Covers: CySA+ Domain 3 (Vulnerability Management) + CSSP Infrastructure Support requirement (vulnerability scanning & remediation planning).
