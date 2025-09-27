

# Detections & Queries

## SSH Brute Force (ATT&CK T1110.001)
**KQL:**
`event.module:"zeek" and event.dataset:"zeek.ssh" and ssh.auth.success:false`                                                                                    
**Rule idea:** >20 failures by same `source.ip` in 5m


## DNS Tunneling (ATT&CK T1071.004)
**KQL (noise):**
`event.module:"zeek" and event.dataset:"zeek.dns" and zeek.dns.rcode_name:NXDOMAIN"`                                                                      
**Additonal:** high-entropy subdomains, spikes per `source.ip`


## Suricata High/Med Alerts
**KQL:**
`event.module:suricata and suricata.eve.alert.serverity >=2`
