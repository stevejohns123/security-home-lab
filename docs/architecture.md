# Lab Architecture

## Environment Overview

This lab simulates a small enterprise network with a Splunk SIEM deployment monitoring authentication activity for signs of brute-force attacks.

## Components

| Component | Role | Notes |
|---|---|---|
| Splunk Enterprise (Free/Trial license) | Central log ingestion, indexing, search, and dashboarding | Single-instance deployment |
| Simulated client/server hosts | Generate authentication events (success/failure) | Synthetic log data, no real credentials or PII |
| Custom index: `auth_logs` | Stores authentication event data | Sourcetype: `auth_events` |

## Data Flow

1. **Log Generation** — Authentication events (login attempts, successes, and failures) are generated from simulated hosts representing a small network of servers/workstations.
2. **Ingestion** — Logs are forwarded into Splunk and indexed under `auth_logs`.
3. **Field Extraction** — Key fields (`src_ip`, `user`, `action`, `reason`, `host`) are extracted at index time for use in SPL queries.
4. **Detection** — Custom SPL searches (see [`spl-queries/`](../spl-queries/)) run against the indexed data to identify brute-force patterns.
5. **Visualization** — Detection results feed into dashboards for analyst triage (attack frequency, top source IPs, failure heatmap).

## Design Rationale

The lab intentionally focuses on **authentication logs** first because credential-based attacks (brute force, password spraying, credential stuffing) are among the most common initial-access techniques observed in real-world incidents, and they map cleanly to a single, well-documented MITRE ATT&CK technique (T1110), making them a strong first detection to build and document end-to-end.

## Planned Expansion

- Add a Windows Server + Active Directory VM to generate authentic domain authentication logs
- Install Sysmon on client endpoints for process-level visibility (enables detections beyond auth failures — e.g., suspicious process execution, lateral movement)
- Use Atomic Red Team to simulate realistic attacker behavior in a controlled way, rather than only synthetic log data
