# Elastic and Wazuh Detection Operations Workbook

Public portfolio artifact for SOC, SIEM, MDR, detection, and log-analysis review.

Best reviewed for: SOC Analyst, SIEM Analyst, MDR Analyst, Detection Analyst, Security Analyst, Wazuh, Elastic, and Logstash roles.

## Summary

This workbook demonstrates an end-to-end Elastic and Wazuh security operations workflow:

- Logstash collection and parsing
- Timestamp normalization
- Kibana validation
- Wazuh decoder inspection
- Custom Wazuh rule engineering
- Field-level rule troubleshooting
- KQL and Lucene investigation patterns
- Apache log attack reconstruction
- Sanitized analyst documentation

The core skill demonstrated is turning raw events into validated fields, validated fields into detections, detections into focused queries, and focused queries into defensible incident narratives.

---

## What this proves

| Capability | Evidence |
|---|---|
| Log ingestion and parsing | Logstash pipeline, auth log ingestion, Grok parsing, Date filter normalization, Kibana validation |
| Detection engineering | Wazuh decoder inspection, custom rules, parent-child rule logic, corrected alert validation |
| Troubleshooting discipline | Failed custom rule, decoded-field inspection, corrected field selection, retest evidence |
| Query fluency | KQL exact filters, wildcards, numeric/date ranges, Lucene regex, fuzzy search, proximity search |
| Attack reconstruction | Attacker source identification, tool sequence, brute force, upload activity, web shell execution, LFI, database access |
| Public-safe reporting | Sanitized screenshots, redacted credentials, query ledgers, reviewer proof map, source files |

---

## Evidence index

| Evidence | What it shows |
|---|---|
| [Parsed Linux authentication event](screenshots/01-logstash-collection-processing-transformation/04-kibana-auth-logs-useradd-event-validation.png) | Logstash pipeline output validated in Kibana |
| [Decoded Wazuh fields](screenshots/02-wazuh-custom-alert-rule-engineering/12-wazuh-auditd-decoded-fields-for-custom-rule-troubleshooting.png) | Field-level troubleshooting before rule correction |
| [Corrected custom Wazuh rule validation](screenshots/02-wazuh-custom-alert-rule-engineering/14-wazuh-auditd-custom-rule-100002-corrected-validation.png) | Custom rule fires after matching the correct decoded field |
| [Lucene regex investigation](screenshots/03-elastic-query-languages-investigation-patterns/21-kibana-incidents-ransomware-comment-client-list-lucene-regex-filter.png) | Query-language precision using analyst-comment regex |
| [Attacker source identification](screenshots/04-slingshot-attack-reconstruction/30-kibana-slingshot-remote-address-distribution-attacker-identification.png) | Dominant source IP identified through field statistics |
| [First web shell command](screenshots/04-slingshot-attack-reconstruction/38-kibana-slingshot-first-web-shell-command.png) | Web shell execution evidence from Apache logs |

---

## Fast review path

| Step | Review |
|---|---|
| 1 | [Reviewer proof map](reviewer-proof-map.md) |
| 2 | [Docs index](docs/README.md) |
| 3 | [Section 02 - Wazuh custom alert rule engineering](docs/02-wazuh-custom-alert-rule-engineering.md) |
| 4 | [Section 04 - Slingshot attack reconstruction](docs/04-slingshot-attack-reconstruction.md) |
| 5 | [Wazuh rules](configs/wazuh/local_rules.xml) |
| 6 | [Slingshot investigation queries](queries/section-04-slingshot-investigation-queries.md) |

---

## Workbook sections

| Section | Focus | Primary proof |
|---|---|---|
| [01 - Logstash Collection, Processing, and Transformation](docs/01-logstash-collection-processing-transformation.md) | Pipeline layer | Logstash service, auth log pipeline, Grok parsing, timestamp normalization, Kibana validation |
| [02 - Wazuh Custom Alert Rule Engineering](docs/02-wazuh-custom-alert-rule-engineering.md) | Detection layer | Decoder inspection, custom rules, failed rule troubleshooting, corrected rule validation |
| [03 - Elastic Query Languages and Investigation Patterns](docs/03-elastic-query-languages-investigation-patterns.md) | Query layer | KQL filters, Lucene regex, fuzzy search, proximity search, range queries |
| [04 - Slingshot Attack Reconstruction](docs/04-slingshot-attack-reconstruction.md) | Investigation layer | Apache log pivots, attacker identification, tool sequence, brute force, upload, web shell, LFI, database access |
| [05 - Advanced ELK Recap and Analyst Lessons](docs/05-advanced-elk-recap-analyst-lessons.md) | Synthesis layer | Transferable lessons across ingestion, detection, query, and investigation work |

---

## Technical source files

| File | Purpose |
|---|---|
| [configs/logstash/auth.conf](configs/logstash/auth.conf) | Public-safe Logstash pipeline configuration |
| [configs/wazuh/local_rules.xml](configs/wazuh/local_rules.xml) | Custom Wazuh rule logic |
| [queries/section-03-kql-lucene-queries.md](queries/section-03-kql-lucene-queries.md) | KQL and Lucene query ledger |
| [queries/section-04-slingshot-investigation-queries.md](queries/section-04-slingshot-investigation-queries.md) | Slingshot investigation query ledger |

---

## Strongest proof points

## 1. Logstash operational pipeline

This section shows Logstash installed, enabled, configured, and validated. The pipeline ingests Linux authentication logs, parses fields with Grok, normalizes timestamps, outputs to Elasticsearch, and is validated in Kibana.

Review:

- [Section 01 documentation](docs/01-logstash-collection-processing-transformation.md)
- [Public-safe Logstash config](configs/logstash/auth.conf)
- [Kibana validation screenshot](screenshots/01-logstash-collection-processing-transformation/04-kibana-auth-logs-useradd-event-validation.png)

## 2. Wazuh rule troubleshooting

This is one of the strongest evidence chains in the workbook.

A custom Wazuh rule initially failed because the logic targeted the wrong decoded field. The decoded event showed the relevant value was in `audit.directory.name`, not `audit.cwd`. The rule was corrected and validated.

Review:

- [Section 02 documentation](docs/02-wazuh-custom-alert-rule-engineering.md)
- [Decoded-field troubleshooting screenshot](screenshots/02-wazuh-custom-alert-rule-engineering/12-wazuh-auditd-decoded-fields-for-custom-rule-troubleshooting.png)
- [Corrected rule validation screenshot](screenshots/02-wazuh-custom-alert-rule-engineering/14-wazuh-auditd-custom-rule-100002-corrected-validation.png)
- [Custom Wazuh rules](configs/wazuh/local_rules.xml)

## 3. KQL and Lucene investigation patterns

This section demonstrates practical query-language fluency across exact filters, wildcards, boolean logic, numeric ranges, date boundaries, regex, fuzzy search, and proximity search.

Review:

- [Section 03 documentation](docs/03-elastic-query-languages-investigation-patterns.md)
- [KQL and Lucene query ledger](queries/section-03-kql-lucene-queries.md)

## 4. Slingshot attack reconstruction

This section reconstructs a web-application attack path from Apache log evidence.

The investigation path includes attacker source identification, scanner activity, directory enumeration, admin login brute force, upload activity, web shell execution, LFI, and database/table access.

Review:

- [Section 04 documentation](docs/04-slingshot-attack-reconstruction.md)
- [Slingshot query ledger](queries/section-04-slingshot-investigation-queries.md)
- [Attacker source identification screenshot](screenshots/04-slingshot-attack-reconstruction/30-kibana-slingshot-remote-address-distribution-attacker-identification.png)
- [First web shell command screenshot](screenshots/04-slingshot-attack-reconstruction/38-kibana-slingshot-first-web-shell-command.png)

---

## Repository structure

| Path | Purpose |
|---|---|
| README.md | Reviewer-facing front door |
| reviewer-proof-map.md | Claim-to-evidence map |
| docs/ | Section-level documentation |
| configs/ | Public-safe Logstash and Wazuh source files |
| queries/ | KQL, Lucene, and investigation query ledgers |
| screenshots/ | Sanitized visual evidence |

---

## Public-safety scope

This repository is public-safe and sanitized.

Included:

- Sanitized Logstash config
- Wazuh XML rule logic
- Kibana screenshots
- KQL and Lucene queries
- Result counts
- Field-statistics screenshots
- Analyst notes and lessons

Excluded:

- Flags
- Credentials
- Raw passwords
- Authorization headers
- Sensitive request bodies
- Database credentials
- Internal answer material
- Any screenshot exposing sensitive material

---

## Role alignment

This workbook is most relevant to:

- SOC Analyst
- MDR Analyst
- SIEM Analyst
- Detection Analyst
- Security Analyst
- Log Analysis Analyst
- Wazuh Analyst
- Elastic Analyst
- Security Operations Analyst

---

## Related portfolio

- [Main GitHub profile](https://github.com/gabrielmarquezcyber)
- [Elastic SIEM Detection Engineering and Vulnerability Risk Automation](https://github.com/gabrielmarquezcyber/elastic-siem-detection-vuln-prioritization)
- [SOC Analyst Splunk Operations Workbook](https://github.com/gabrielmarquezcyber/soc-analyst-splunk-operations-workbook)
- [Azure Cloud Security Governance](https://github.com/gabrielmarquezcyber/azure-cloud-security-governance)
