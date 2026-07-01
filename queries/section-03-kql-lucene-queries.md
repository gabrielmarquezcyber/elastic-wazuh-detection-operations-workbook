# Section 03 Query Ledger - Elastic Query Languages and Investigation Patterns

## Purpose

This file preserves the exact KQL and Lucene queries used for the Elastic investigation-pattern section.

## Query ledger

| Pattern | Exact query | Result |
|---|---|---|
| KQL exact nested-field filtering | `affected_systems.affected_files.file_name: "marketing_strategy_2023_07_23.pptx"` | 4 hits |
| KQL wildcard file-family filtering | `affected_systems.system_type: "File Server" AND affected_systems.affected_files.file_name: marketing_strategy*` | 135 hits |
| KQL boolean pivot for affected web server | `affected_systems.system_type: "Web Server" AND incident_comments: "true positive" AND affected_systems.logged_on_users: ("admin" AND "it")` | 1 hit; web-server-77 |
| Lucene regex against analyst comments and file names | `incident_comments: /.*ransomware.*/ AND affected_systems.affected_files.file_name: /.*client_list.*/` | 69 hits |
| Lucene regex plus analyst pivot | `affected_systems.affected_files.file_name: /.*project.*/ AND team_members.name: "EVenis"` | 81 hits; latest affected system web-server-37 |
| KQL numeric range | `incident_type: "Data Leak" AND severity_level >= 9` | 52 hits |
| KQL date boundary and asset-type filtering | `team_members.name: "AJohnston" AND @timestamp < "2022-12-02" AND affected_systems.system_type: ("Email Server" OR "Web Server")` | 65 hits |
| KQL incident-ID range and analyst comment evidence | `incident_id >= 1 AND incident_id <= 500 AND incident_type: "Data Leak" AND affected_systems.system_name: "file-server-65" AND incident_comments: "false positive"` | 1 hit; analyst JLim |
| Lucene fuzzy search | `team_members.name: "JLim" AND incident_comments: true~1` | 110 hits |
| Lucene proximity search | `incident_comments: "data leak true negative"~3` | 33 hits |
| Lucene proximity search with analyst filter | `team_members.name: "AJohnston" AND incident_comments: "detected negative"~2` | 40 hits |

## Analyst lesson

Similar concepts can produce different result counts depending on the evidence field queried. In this section, searching structured incident type and searching analyst comment text produced different results. The accepted investigation path used analyst comment text.