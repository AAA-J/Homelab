

# SIEM Lab Runbook


## Scope
Zeek + Suricata + Filebeat -> Elasticsearch -> Kibana. Lab VLANs, Kali sensor, Mint victim, WinOS attacker.


## Daily Checks
- Kibana "SOC Home" loads
- ES health: green/yellow; shards OK
- Filebeat service healthy
- Suricata/Zeek logs updating


## Triage Flow
1) **Alert/Dashboard spike** (e.g., Suricata signature or NXDOMAIN ratio)
2) **Investigate** in Discover (KQL, add fields)
3) **Scope**: other hosts, time, ports, domains
4) **Contain** (lab): block in OPNsense, kill process, stop service
5) **Document** in `detections.md` + playbooks
6) **Lessons learned**: tune rules, add dashboards/dectections


## Contacts / Assets
- Sensor IPs, VLANS, admin creds (stored in password manager)
