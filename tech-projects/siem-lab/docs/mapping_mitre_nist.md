

# Mapping: MITRE ATT&CK NIST 800-53


## MITRE ATT&CK
- **T1110** Brute Force (SSH) -> simulated via plink loops from WinOS
- **T1071.004** Application Layer Protocol: DNS (Tunneling) -> simulated via iodine / random subdomains


## NIST SP 800-53 Rev.5 (selected)
- **AU-6 Audit Review** -> Analysts review Discover & dashboards; `detections.md`
- **SI-4 System Monitoring** -> Suricata + Zeek sensors generate telemetry & alerts


## Process
**Detection -> Investigation (queries) -> Containment (lab action) -> Lessons learned (dashboard/rule updates)**


## Hygiene
- Store passwords in a local password manager
- Never commit secrets; use `.gitignore` and `.example.yml`
- Optional: add `.env.example` with placeholders
