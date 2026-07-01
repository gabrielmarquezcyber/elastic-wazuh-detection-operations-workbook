# Reviewer Proof Map

## Purpose

This proof map connects the workbook's technical claims to supporting screenshots, configuration files, rule files, query ledgers, and section documentation.

The root README is the primary visual review path. This file is the audit path for reviewers who want to map each claim to evidence.

## Fast evidence map

| Claim | Evidence | Source of truth |
|---|---|---|
| Logstash can collect, parse, normalize, and route Linux authentication logs into Elasticsearch. | Screenshots 01-05 | [configs/logstash/auth.conf](configs/logstash/auth.conf), [Section 01](docs/01-logstash-collection-processing-transformation.md) |
| Wazuh custom rules can be tested, troubleshot, corrected, and validated through decoded-field inspection. | Screenshots 06-17 | [configs/wazuh/local_rules.xml](configs/wazuh/local_rules.xml), [Section 02](docs/02-wazuh-custom-alert-rule-engineering.md) |
| Elastic KQL and Lucene can support precise SOC-style investigation pivots. | Screenshots 18-28 | [queries/section-03-kql-lucene-queries.md](queries/section-03-kql-lucene-queries.md), [Section 03](docs/03-elastic-query-languages-investigation-patterns.md) |
| Apache log evidence can be used to reconstruct a web-application compromise. | Screenshots 29-40 | [queries/section-04-slingshot-investigation-queries.md](queries/section-04-slingshot-investigation-queries.md), [Section 04](docs/04-slingshot-attack-reconstruction.md) |
| The workbook synthesizes pipeline, detection, query, and reconstruction lessons into role-relevant analyst takeaways. | Section 05 | [Section 05](docs/05-advanced-elk-recap-analyst-lessons.md) |

## Section 01 - Logstash Collection, Processing, and Transformation

| Screenshot | What it proves |
|---|---|
| 01-logstash-installed-service-active.png | Logstash installed, enabled, and active as a service. |
| 02-logstash-auth-conf-redacted-pipeline-config.png | Public-safe Logstash auth pipeline configuration. |
| 03-logstash-auth-pipeline-service-restarted-active.png | Pipeline service restarted and active after configuration. |
| 04-kibana-auth-logs-useradd-event-validation.png | Parsed useradd event visible in Kibana. |
| 05-kibana-auth-logs-passwd-event-validation.png | Parsed passwd event visible in Kibana. |

Supporting source:

- [configs/logstash/auth.conf](configs/logstash/auth.conf)

## Section 02 - Wazuh Custom Alert Rule Engineering

| Screenshot | What it proves |
|---|---|
| 06-wazuh-sysmon-decoder-logtest-validation.png | Wazuh logtest decoding and rule filtering. |
| 07-wazuh-sysmon-svchost-rule-match-validation.png | Specific Sysmon suspicious-process rule match. |
| 08-wazuh-sysmon-taskhost-rule-match-validation.png | Alternate suspicious-process rule match. |
| 09-wazuh-sysmon-if-sid-parent-child-rule-order-validation.png | Parent-child rule order using if_sid. |
| 10-wazuh-local-audit-custom-rule-100002-definition.png | Initial custom local audit rule definition. |
| 11-wazuh-auditd-default-rule-80790-before-field-correction.png | Default rule match before custom-rule correction. |
| 12-wazuh-auditd-decoded-fields-for-custom-rule-troubleshooting.png | Decoded fields used to troubleshoot the custom rule. |
| 13-wazuh-local-audit-custom-rule-100002-field-correction.png | Corrected field selection. |
| 14-wazuh-auditd-custom-rule-100002-corrected-validation.png | Corrected custom rule match. |
| 15-wazuh-auditd-fine-tuned-custom-rule-chain-definition.png | Fine-tuned child-rule chain. |
| 16-wazuh-auditd-test-php-rule-match-validation.png | Suspicious extension rule match. |
| 17-wazuh-auditd-malware-checker-sh-rule-match-validation.png | Suspicious file-name rule match. |

Supporting source:

- [configs/wazuh/local_rules.xml](configs/wazuh/local_rules.xml)

## Section 03 - Elastic Query Languages and Investigation Patterns

| Screenshot | What it proves |
|---|---|
| 18-kibana-incidents-exact-file-name-kql-filter.png | Exact nested-field KQL filtering. |
| 19-kibana-incidents-file-server-marketing-strategy-wildcard-kql-filter.png | KQL wildcard and asset-type filtering. |
| 20-kibana-incidents-web-server-true-positive-admin-it-kql-filter.png | Boolean and nested-field investigation pivot. |
| 21-kibana-incidents-ransomware-comment-client-list-lucene-regex-filter.png | Lucene regex against analyst comments and file names. |
| 22-kibana-incidents-project-file-evenis-latest-system-lucene-regex-filter.png | Regex plus analyst pivot and newest-result extraction. |
| 23-kibana-incidents-data-leak-severity-range-kql-filter.png | Numeric range filtering. |
| 24-kibana-incidents-ajohnston-email-web-server-date-range-kql-filter.png | Date boundary and asset-type filtering. |
| 25-kibana-incidents-id-range-file-server-65-false-positive-kql-filter.png | Incident-ID range and analyst comment evidence. |
| 26-kibana-incidents-jlim-true-fuzzy-lucene-filter.png | Lucene fuzzy search. |
| 27-kibana-incidents-data-leak-true-negative-proximity-lucene-filter.png | Lucene proximity search. |
| 28-kibana-incidents-ajohnston-detected-negative-proximity-lucene-filter.png | Proximity search combined with analyst filter. |

Supporting source:

- [queries/section-03-kql-lucene-queries.md](queries/section-03-kql-lucene-queries.md)

## Section 04 - Slingshot Attack Reconstruction

| Screenshot | What it proves |
|---|---|
| 29-kibana-slingshot-apache-logs-initial-scope-field-discovery.png | Initial field discovery for Apache log investigation. |
| 30-kibana-slingshot-remote-address-distribution-attacker-identification.png | Attacker IP identification through field statistics. |
| 31-kibana-slingshot-attacker-user-agent-scanner-identification.png | Tooling sequence from user-agent distribution. |
| 32-kibana-slingshot-attacker-404-response-count.png | Attacker 404 response count during enumeration. |
| 33-kibana-slingshot-gobuster-discovered-paths-non-404.png | Successful directory discovery evidence. |
| 34-kibana-slingshot-gobuster-admin-login-page-discovery.png | Admin-login discovery through Gobuster and 401 response. |
| 35-kibana-slingshot-hydra-admin-panel-bruteforce-evidence.png | Hydra brute-force activity. |
| 36-kibana-slingshot-hydra-successful-admin-login-sanitized.png | Sanitized successful login evidence. |
| 37-kibana-slingshot-admin-upload-activity.png | Post-login upload activity. |
| 38-kibana-slingshot-first-web-shell-command.png | First observed web shell command. |
| 39-kibana-slingshot-lfi-config-db-file-access.png | LFI-style access to config-db.php. |
| 40-kibana-slingshot-phpmyadmin-customer-credit-cards-database-access.png | phpMyAdmin database and table access. |

Supporting source:

- [queries/section-04-slingshot-investigation-queries.md](queries/section-04-slingshot-investigation-queries.md)

## Evidence safety scope

This repository excludes sensitive authentication material, private exercise artifacts, raw request bodies containing sensitive material, credential-bearing values, and screenshots that do not add reviewer-facing analyst proof.

Public screenshots were selected for analyst evidence value and sanitized where needed.