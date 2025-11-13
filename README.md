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

# Threat Intelligence Lab — VirusTotal Log Enricher

## Objective
Automate IP address reputation checks using the VirusTotal API, enrich indicators of compromise (IOCs), and generate CSV-based threat intelligence reports to support SOC investigations.

## Tools Used
- Python 3
- VirusTotal Public API
- CSV (for reporting)

## Skills Learned
- Working with REST APIs in Python
- Automating threat intelligence enrichment workflows
- Parsing text input files and handling JSON API responses
- Exporting structured data to CSV for analysis
- Supporting Tier 1 SOC investigations with enrichment tooling

## Steps Overview
1. Obtain a free VirusTotal API key and configure it in `enrich.py` (`API_KEY = "YOUR_API_KEY_HERE"`).
2. Prepare an input file (`sample_ips.txt`) containing one IP address per line.
3. From the `threat-intel-enricher` folder, run `python enrich.py sample_ips.txt`.
4. For each IP address, query the VirusTotal API for reputation and malicious score.
5. Write enrichment results to `enriched_results.csv` with columns such as `ip` and `malicious_score`.
6. Open the CSV file in Excel, Power BI, or another BI tool to review, sort, and visualize threat levels across IP addresses.

## Results
- Built a Python-based enrichment tool that automates IP reputation lookups using VirusTotal.
- Successfully processed lists of IP addresses and generated `enriched_results.csv` as a clean report.
- Provided a simple way for analysts to quickly assess which IPs may be malicious or suspicious.
- Demonstrated an end-to-end enrichment workflow similar to real SOC processes.

## Next Steps
- Add support for domains and URLs in addition to IP addresses.
- Include additional VirusTotal attributes (e.g., categories, detection ratios, last analysis date).
- Integrate with other threat intelligence providers (AbuseIPDB, GreyNoise, etc.) for multi-source enrichment.
- Build a small Streamlit dashboard to visualize malicious scores and filter IOCs interactively.

---

# SOC Lab — Incident Report Generator (Python & Markdown)

## Objective
Automate the creation of standardized SOC incident reports using Python and Markdown templates to streamline post-incident documentation and ensure consistent report formats.

## Tools Used
- Python 3
- Markdown templates
- `datetime` module

## Skills Learned
- SOC incident documentation and reporting workflows
- Template-based content generation and automation
- Using Python to fill placeholders and insert timestamps
- Structuring incident reports with consistent sections (Summary, Indicators, Affected Systems, Actions)

## Steps Overview
1. Create Markdown templates for incident types (e.g., `templates/brute_force.md`, `templates/malware.md`) with placeholders such as `{{date}}`.
2. Implement `generate.py` to:
   - Read the selected template based on the incident type argument (e.g., `brute_force`, `malware`).
   - Replace `{{date}}` with the current timestamp.
   - Write the output to a new file (e.g., `incident_brute_force.md`, `incident_malware.md`).
3. From the `incident-generator` folder, run `python generate.py brute_force` or `python generate.py malware`.
4. Review the generated Markdown incident report and add case-specific details if needed.
5. Store the reports in a central location or convert them to PDF for sharing with stakeholders.

## Results
- Successfully generated consistent SOC incident reports using predefined templates.
- Automated insertion of timestamps and standardized sections (Summary, Indicators, Affected Systems, Recommended Actions).
- Created reusable report structures for common incident types such as brute-force attacks and malware detections.
- Simulated a realistic incident response documentation workflow used by SOC analysts.

## Next Steps
- Add more incident types (phishing, ransomware, data exfiltration, insider threat).
- Allow passing incident metadata (affected IPs, users, hosts) via JSON input or command-line arguments.
- Integrate a Markdown-to-PDF conversion step to produce final, shareable incident reports.
- Connect the generator to a ticketing system (Jira, ServiceNow, etc.) to automatically attach generated reports to incident tickets.

