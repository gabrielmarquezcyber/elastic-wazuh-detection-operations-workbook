# Docs Index

## Primary review path

Start with the root [README](../README.md). It provides the visual proof narrative and links to the strongest reviewer evidence.

Use this docs index for deeper review by section.

## Section docs

| Section | Focus |
|---|---|
| [01 - Logstash Collection, Processing, and Transformation](01-logstash-collection-processing-transformation.md) | Logstash service validation, Linux auth log ingestion, Grok parsing, timestamp normalization, and Kibana validation. |
| [02 - Wazuh Custom Alert Rule Engineering](02-wazuh-custom-alert-rule-engineering.md) | Decoder inspection, custom rules, field mismatch troubleshooting, child-rule tuning, and alert validation. |
| [03 - Elastic Query Languages and Investigation Patterns](03-elastic-query-languages-investigation-patterns.md) | KQL, Lucene, exact filters, wildcards, ranges, regex, fuzzy search, and proximity search. |
| [04 - Slingshot Attack Reconstruction](04-slingshot-attack-reconstruction.md) | Apache log investigation, attacker identification, tool pivots, brute force, upload, web shell, LFI, and database access. |
| [05 - Advanced ELK Recap and Analyst Lessons](05-advanced-elk-recap-analyst-lessons.md) | Transferable lessons across pipeline, detection, query, and attack-reconstruction workflows. |

## Source files

| File | Purpose |
|---|---|
| [Logstash auth pipeline](../configs/logstash/auth.conf) | Public-safe Logstash pipeline configuration for Linux authentication log ingestion. |
| [Wazuh local rules](../configs/wazuh/local_rules.xml) | Custom Wazuh auditd rule chain used for validation. |
| [Section 03 query ledger](../queries/section-03-kql-lucene-queries.md) | Exact KQL and Lucene queries from the Elastic query-language section. |
| [Section 04 query ledger](../queries/section-04-slingshot-investigation-queries.md) | Exact Elastic queries used for Slingshot attack reconstruction. |

## Evidence archive

| Folder | Contents |
|---|---|
| [Section 01 screenshots](../screenshots/01-logstash-collection-processing-transformation/) | Logstash service, pipeline, restart, and Kibana validation evidence. |
| [Section 02 screenshots](../screenshots/02-wazuh-custom-alert-rule-engineering/) | Wazuh decoder, rule, troubleshooting, correction, and child-rule validation evidence. |
| [Section 03 screenshots](../screenshots/03-elastic-query-languages-investigation-patterns/) | KQL and Lucene query validation evidence. |
| [Section 04 screenshots](../screenshots/04-slingshot-attack-reconstruction/) | Apache log investigation and attack-reconstruction evidence. |

## Audit path

Use the [reviewer proof map](../reviewer-proof-map.md) to map claims to screenshots and source files.