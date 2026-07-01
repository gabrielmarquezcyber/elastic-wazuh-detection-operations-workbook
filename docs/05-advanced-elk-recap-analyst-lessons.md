# Section 05 - Advanced ELK Recap and Analyst Lessons

[README](../README.md) | [Docs Index](README.md) | [Proof Map](../reviewer-proof-map.md)

## Purpose

This section synthesizes the workbook into transferable SOC analyst lessons.

Sections 01-04 provide the evidence. This section connects those evidence blocks into a practical operating model for Elastic and Wazuh security operations.

Core thesis:

The durable skill is not memorizing syntax. The durable skill is turning raw events into validated fields, validated fields into detections, detections into focused queries, and focused queries into defensible incident narratives.

## Workbook operating model

| Layer | Section | Practical result |
|---|---|---|
| Pipeline | Section 01 | Raw logs become parsed, timestamp-normalized Elastic events. |
| Detection | Section 02 | Decoded fields become custom Wazuh rule logic and validated alerts. |
| Query | Section 03 | Indexed data becomes focused KQL and Lucene investigation evidence. |
| Investigation | Section 04 | Scattered Apache log events become a coherent attack timeline. |

## Pipeline layer lesson

Section 01 showed that search quality depends on pipeline quality.

Workflow:

| Step | Result |
|---|---|
| Logstash file input | Linux authentication logs were collected. |
| Grok parsing | Raw log messages became structured fields. |
| Date filter | Source event time was normalized into `@timestamp`. |
| Elasticsearch output | Parsed events were routed to an `auth-logs-*` index pattern. |
| Kibana validation | Parsed authentication events became searchable analyst evidence. |

Analyst lesson:

Bad parsing creates bad analysis. Structured fields and normalized timestamps make investigation faster, cleaner, and more defensible.

## Detection layer lesson

Section 02 showed that custom detection logic depends on decoded-field validation.

Workflow:

| Step | Result |
|---|---|
| Wazuh logtest | Raw events were decoded and evaluated against rules. |
| Default rule review | Existing rule behavior was observed before custom tuning. |
| Custom rule creation | Local rule 100002 extended auditd file-creation logic. |
| Field mismatch troubleshooting | `audit.cwd` failed because the target value appeared in `audit.directory.name`. |
| Rule correction | Rule 100002 fired after matching the correct decoded field. |
| Child-rule tuning | Rules 100003-100006 escalated, classified, and suppressed specific conditions. |

Analyst lesson:

A rule can be syntactically valid and still fail if it matches the wrong decoded field. Decoder output must be inspected before rule logic is trusted.

## Query layer lesson

Section 03 showed that query language choice should follow the investigation need.

| Query need | Useful pattern |
|---|---|
| Exact artifact lookup | KQL exact field filtering. |
| File-family expansion | KQL wildcard matching. |
| Combined evidence conditions | KQL boolean logic. |
| Severity or ID scoping | KQL numeric ranges. |
| Time scoping | KQL date boundaries. |
| Flexible text patterns | Lucene regex. |
| Near matches | Lucene fuzzy search. |
| Related terms near each other | Lucene proximity search. |

Analyst lesson:

The same concept can return different results depending on the evidence field queried. Field selection and time range control matter before result counts are trusted.

## Investigation layer lesson

Section 04 showed how individual log events become an incident narrative.

Workflow:

| Step | Result |
|---|---|
| Field discovery | The useful source field was identified before investigation pivots. |
| Source distribution | The attacker IP was identified through field statistics. |
| User-agent analysis | Tool sequence was inferred from user-agent distribution. |
| Enumeration review | Gobuster behavior and 404 counts were validated. |
| Authentication review | Hydra brute-force activity and successful login evidence were separated. |
| Upload review | Post-login upload activity was tied to uploaded file access. |
| Command execution review | The first web shell command was identified. |
| LFI review | Path traversal to `config-db.php` was confirmed. |
| Database access review | phpMyAdmin database and table access were identified. |
| Timeline building | Evidence was ordered into a defensible incident narrative. |

Analyst lesson:

A SOC analyst is not only searching logs. The analyst must turn scattered evidence into a defensible timeline and explain what each evidence point proves.

## Cross-platform SOC value

This workbook complements Splunk-focused work by demonstrating a second SIEM ecosystem.

| Platform area | Demonstrated capability |
|---|---|
| Splunk-focused work | SPL searches, ingestion validation, dashboards, parsing repair, and field extraction. |
| Elastic and Wazuh work | Logstash pipelines, Grok parsing, Wazuh custom rules, KQL and Lucene searches, and Apache log attack reconstruction. |

Analyst lesson:

The durable skill is not tool loyalty. The durable skill is understanding how logs move, how fields are created, how detections are validated, how queries narrow evidence, and how investigations become reports.

## Final takeaway

This workbook demonstrates practical SOC workflow across ingestion, parsing, detection, query, and reconstruction layers using Elastic and Wazuh evidence.

The strongest portfolio proof points are:

| Proof point | Why it matters |
|---|---|
| Logstash operational pipeline | Shows the ability to create and validate an ingestion and parsing workflow. |
| Wazuh rule troubleshooting | Shows detection engineering judgment, not just rule writing. |
| Elastic query fluency | Shows the ability to ask precise questions against indexed data. |
| Slingshot attack reconstruction | Shows the ability to convert scattered web logs into an incident narrative. |

## Reviewer takeaway

Sections 01-04 provide the evidence. This section explains the transferable analyst model behind that evidence: validate the pipeline, validate decoded fields, validate queries, and validate conclusions through a defensible timeline.