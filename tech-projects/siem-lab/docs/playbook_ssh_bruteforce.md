

# Playbook: SSH Brute Force (ATT&CK T1110.001)

## Trigger
- Dectection rule fires or dashboard spike on failed SSH logins.

## Validate
- Discover KQL: `event.module:"zeel" and event.dataset:'zeek.ssh" and ssh.auth.success:false`
- Add columns: source.ip, destination.ip, user, @timestamp

## Scope
- Top source.ip
- Target hosts
- Any subsequent `ssh.auth.success:true`?

## Containment (Lab)
- Block source in OPNsense (temporal rule)
- If target is lab VM: disable password auth temporarily

## Recovery
- Rotate creds on target if a success observed
- Re-enable password auth after test if desired

## Lessons Learned
- Create/adjust detection thresholds
- add "SSH Brute Force" dashboard widgets
