# SIEM Lab — Elastic Stack

## Objective
Build a lightweight SIEM using the Elastic Stack (Elasticsearch + Kibana) to ingest Linux authentication logs, detect brute-force attacks, and practice SOC alerting, investigation, and dashboard creation.

## Tools Used
- Elasticsearch
- Kibana
- Docker
- Linux authentication logs
- NDJSON detection rules

## Skills Learned
- SIEM deployment and configuration with Elastic Stack
- Log ingestion and index pattern creation
- Detection engineering (custom brute-force rules)
- Alert triage and investigation in a SIEM
- Dashboard and visualization building in Kibana

## Steps Overview
1. Deploy Elasticsearch and Kibana using Docker Compose from the `siem-lab` folder (`docker-compose up -d`).
2. Open Kibana at `http://localhost:5601` and use Discover → “Upload file” to ingest `logs/failed_logins.log`.
3. Create an index pattern (e.g., `auth-logs-*`) and verify failed login events in Discover.
4. Go to Security → Alerts → Manage Rules and import `rules/brute_force_rule.ndjson`.
5. Enable the brute-force detection rule and run it against the `auth-logs-*` index.
6. View alerts under Security → Alerts & Insights → Alerts, filter by the rule name, and analyze source IPs and timestamps.
7. Build a Kibana dashboard that visualizes failed logins, source IP distribution, and generated alerts.

## Results
- Successfully deployed Elasticsearch and Kibana via Docker.
- Ingested Linux authentication logs and confirmed visibility in Kibana Discover.
- Custom brute-force detection rule generated alerts based on repeated failed login attempts.
- Performed basic SOC-style alert investigation using the Kibana Security interface.
- Created an initial detection dashboard to monitor authentication activity and brute-force patterns.

## Next Steps
- Add Filebeat for automated log shipping from Linux VMs.
- Ingest additional log sources (web server, firewall, endpoint security logs).
- Create multiple detection rules to cover other attack behaviors (lateral movement, privilege escalation, anomalous logins).
- Expand dashboards into a more complete SOC view with multiple visualizations and metrics.

---
