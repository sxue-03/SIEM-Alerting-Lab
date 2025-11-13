README 1 — SIEM Alerting Lab (Elastic Stack)
SIEM Alerting Lab (Elastic Stack)

This project demonstrates how to build a lightweight SIEM environment using the Elastic Stack (Elasticsearch + Kibana) to ingest logs, create detection rules, and simulate a real SOC alert workflow.

Overview

The objective of this lab is to deploy a functional SIEM using Docker, ingest authentication logs, create a custom detection rule for brute-force attacks, and generate visualizations inside Kibana.

This simulates SOC processes such as detection engineering, alert investigation, and dashboard creation.

Objectives

Deploy Elasticsearch and Kibana using Docker

Ingest Linux authentication logs

Create and test a brute-force detection rule

Generate alerts and analyze event details

Build a detection dashboard in Kibana

Tools Used
Tool	Purpose
Elasticsearch	Log indexing and search engine
Kibana	Visualization, alerting, SIEM UI
Docker	Rapid environment deployment
Linux logs	Log source for detection
NDJSON rules	Custom detection rule format
Project Structure

siem-lab/
│── docker-compose.yml
│── logs/
│ ├── failed_logins.log
│── rules/
│ ├── brute_force_rule.ndjson
│── README.md

Setup Instructions
1. Start Elastic Stack

From inside the siem-lab folder, run:

docker-compose up -d

Kibana will be available at:

http://localhost:5601

2. Ingest Logs

Open Kibana in your browser.

Go to Discover → “Upload file”.

Select logs/failed_logins.log.

Create a new index pattern, for example: auth-logs-*

Confirm you can see the failed login messages in Discover.

3. Import Detection Rule

In Kibana, go to: Security → Alerts → Manage Rules.

Click “Import rules”.

Select rules/brute_force_rule.ndjson.

Enable the rule and run it against the auth-logs-* index.

4. View Alerts

Go to: Security → Alerts & Insights → Alerts.

Filter by the rule name, for example “Brute force attack detected”.

Review alert details, source IPs, and timestamps.

Skills Demonstrated

SIEM configuration and setup

Log ingestion pipelines

Detection engineering in a SIEM

SOC alerting workflows

Dashboard creation in Kibana

Future Enhancements

Add Filebeat for automated log shipping from a VM.

Ingest additional log sources (web server logs, firewall logs).

Create multiple detection rules for different attack patterns.

Build a full SOC dashboard with multiple visualizations.
