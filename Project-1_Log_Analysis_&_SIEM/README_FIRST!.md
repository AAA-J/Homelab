# Project 1 Lab Manual — Log Analysis & SIEM (Free & On-Prem)

## 0) Outcome & Success Criteria
By the end you will:
- Mirror VLAN traffic to a monitoring box.
- Run Zeek (network metadata) and Suricata (IDS) on the monitor.
- Ingest Zeek & Suricata logs into ELK (Elasticsearch + Kibana) via Filebeat modules.
- Build dashboards and confirm alerts from simulated attacks (SSH brute force, DNS tunneling, simple phishing beacon).
- Document detection → investigation → response steps with light MITRE ATT&CK and NIST mapping.

**You’ll keep everything local & free** (no Splunk, no cloud trials).

## 1) Reference Architecture (your gear)
- Switch
  - SPAN/Port Mirroring: mirror selected VLANs/ports → monitoring port.
- OPNsense (router/firewall)
  - Normal routing/DHCP for VLAN10/20/30/40/99 etc
- Monitoring box (preferably a dedicated PC/VM with 2+ CPU cores, 8+ GB RAM):
  - Operating System: I.E., Unix; Ubuntu Server 22.04 LTS (recommended) or Debian 12.
  - Runs Zeek, Suricata, Filebeat, Elasticsearch, Kibana (all on the same host is fine to start).
  - NIC connected to monitoring port.
- Test endpoints
  - One Linux VM (Ubuntu) and/or WindowsOS VM on your VLANs to generate benign and malicious test traffic.

# 2) Configure Switch Port Mirroring

# 3) Prepare the Monitoring Host
- 3.1 Operating System baseline
- 3.2 Set the monitor NIC to promiscuous mode

# 4) Install Elasticsearch & Kibana (self-hosted, free)
Elastic 8.x includes security by default (TLS, built-in users). We’ll do a minimal secure single-node.

- 4.1 Install Java (Elastic bundles its own now, but ensure dependencies)
- 4.2 Install Elasticsearch & Kibana
- 4.3 Minimal Elasticsearch config (single node)
  - Start & enable elasticsearch
  - Get the auto-generated elastic user password
  
***Save it securely (password manager / .env not in git)***
- 4.4 Kibana setup
  - Initialize Kibana:
    - Enable kibana
    - Visit https://<monitor_host_ip>:5601 → follow setup prompts to connect to Elasticsearch (you may use the provided enrollment flow). Create your Kibana login. Keep RBAC on (default in 8.x).

# 5) Install Zeek (network metadata)
- Verify the interface (the mirrored one):
- Basic run (test):
- Set Zeek to service mode 
- Enable zeek

***Log location (default): /opt/zeek/logs/current/ (files like conn.log, dns.log, http.log, etc.)***

# 6) Install Suricata (IDS with ET Open rules)
- Enable AF-Packet (best for mirrors)
- Set the interface
- Enable eve.json output
- Pull Emerging Threats Open rules (free)
- Enable suricata

***Tip; Key outputs: /var/log/suricata/eve.json (alerts, DNS, HTTP, TLS metadata, etc.)***

# 7) Install Filebeat & enable Zeek/Suricata modules
- 7.1 Configure Zeek module

***Tip: Edit /etc/filebeat/modules.d/zeek.yml and set log paths***

- 7.2 Configure Suricata module
- 7.3 Point Filebeat to Elasticsearch
- 7.4 Load templates & dashboards; start Filebeat
  - This loads the Zeek and Suricata ingest pipelines and Kibana dashboards automatically.

# 8) Verify Ingestion & Dashboards
- You should see DNS/HTTP flows (Zeek) and alerts/flows (Suricata).

# 9) Generate Test Traffic (safe, local)
- 9.1 Simulate SSH brute force (ATT&CK T1110)
  - From a test Linux VM, attempt bad passwords (against another lab VM that runs SSH)
    - Expectations:
      - Zeek: spikes in conn.log, multiple failed auth sequences (if auth banners visible).
      - Suricata: ET OPEN signatures may flag SSH brute force patterns.

- 9.2 Simulate DNS tunneling behavior (ATT&CK T1071.004)
    - Expectations:
      - Zeek dns.log shows high entropy, many NXDOMAINs.
      - Suricata may flag excessive DNS queries (depends on rules).

***Tip: iodine or dnscat2***

- 9.3 Simulate Suspicious HTTP beacon (TA0011)
    - Expectations:
      - Zeek http.log shows periodic same-host GETs (beacon-like).

# 10) Build Your Kibana Views (analyst workflow)

# 11) Triage & Documentation (CySA+ + DoD-friendly)
***Tip: Detection → Investigation (queries) → Containment (lab action) → Lessons learned (update dashboards/rules)***
- Important hygiene:
  - Store passwords in a local password manager.
  - If you keep configs in git, exclude secrets via .gitignore and sample .env.example.

# 12) Stretch Goals (still free)
- Enrich Zeek DNS with local threat-feeds (plain-text domains/IPs you maintain in git; tag hits in Filebeat ingest).
- Custom Suricata rules for lab IoCs (create a local.rules file and include it in Suricata).
- Packet capture pivots: run tcpdump -i enp3s0 -w /tmp/ssh-bf.pcap during tests and validate with Wireshark → show “packet-to-log” correlation (interview gold).

# 13) Acceptance Checklist

 [&nbsp;&nbsp;] SG250 mirroring to ge9 confirmed.

 [&nbsp;&nbsp;] Zeek logs (conn, dns, http, ssl) rotating in .../logs/current.

 [&nbsp;&nbsp;] Suricata running, ET Open rules loaded, eve.json filling.

 [&nbsp;&nbsp;] Filebeat shipping to Elasticsearch; Kibana dashboards visible.

 [&nbsp;&nbsp;] SSH brute force test produces visible signals (Zeek + Suricata).

 [&nbsp;&nbsp;] DNS anomaly test visible in Zeek DNS (NXDOMAIN / high volume).

 [&nbsp;&nbsp;] At least one Saved Search and one custom Lens viz created.

 [&nbsp;&nbsp;] Runbook + ATT&CK/NIST mapping written in /docs.

