# MITRE ATT&CK Mapping

Mapping detections to a recognized framework like MITRE ATT&CK is standard practice in real SOC environments — it lets analysts communicate findings in a common language and prioritize based on known adversary behavior, rather than describing attacks in ad-hoc terms.

## Technique: T1110 — Brute Force

**Tactic:** Credential Access
**Reference:** https://attack.mitre.org/techniques/T1110/

> Adversaries may use brute force techniques to gain access to accounts when passwords are unknown or when password hashes are obtained.

### Sub-techniques detected in this lab

| Sub-technique | ID | Description | How this lab detects it |
|---|---|---|---|
| Password Guessing | T1110.001 | Repeated attempts against a single known account | Detection flags 5+ failures against the **same username** from one source IP within a 5-minute window |
| Password Spraying | T1110.003 | Attempts using one or few passwords against **many** accounts, to avoid lockout thresholds | Detection flags 5+ failures across **multiple distinct usernames** from one source IP within the same window |

## Why This Detection Matters

Brute-force and password-spraying attacks are frequently the **initial access vector** in larger intrusion chains. Catching this activity early — before an attacker successfully authenticates — gives defenders the opportunity to intervene before an incident escalates to lateral movement or data exfiltration.

## Analyst Triage Workflow

When this detection fires, the recommended triage steps are:

1. **Validate** — confirm the source IP isn't a known false positive (e.g., a misconfigured internal service or a legitimate user who forgot their password)
2. **Scope** — check whether the same source IP appears in other detections (e.g., successful login shortly after failures, which could indicate a successful brute-force)
3. **Contain** — if confirmed malicious, recommend blocking the source IP at the firewall/WAF and forcing a password reset for any targeted accounts
4. **Document** — record the finding, technique mapping, and response in the incident tracker

## Future Technique Coverage

As the lab expands (see [architecture.md](architecture.md#planned-expansion)), planned detections will cover additional ATT&CK techniques, including:

- **T1078** (Valid Accounts) — detecting use of compromised credentials after a successful brute-force
- **T1021** (Remote Services) — detecting lateral movement via RDP/SSH/WinRM
- **T1059** (Command and Scripting Interpreter) — via Sysmon process-execution logging
