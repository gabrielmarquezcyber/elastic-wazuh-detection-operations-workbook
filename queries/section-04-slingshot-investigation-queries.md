# Section 04 Query Ledger - Slingshot Attack Reconstruction

## Purpose

This file preserves the exact Elastic queries used to reconstruct the Slingshot web-application compromise.

## Query ledger

| Investigation step | Exact query or field statistic |
|---|---|
| Initial source-address distribution | `transaction.remote_address: *` |
| Field statistic used for attacker identification | `transaction.remote_address` |
| Attacker user-agent distribution | `transaction.remote_address: "10.0.2.15" AND request.headers.User-Agent: *` |
| Total attacker 404 responses | `transaction.remote_address: "10.0.2.15" AND response.status: 404` |
| Successful directory discoveries excluding sensitive artifacts | `transaction.remote_address: "10.0.2.15" AND request.headers.User-Agent: "Mozilla/5.0 (Gobuster)" AND NOT response.status: 404 AND NOT http.url: /backups*` |
| Protected admin-login discovery | `transaction.remote_address: "10.0.2.15" AND request.headers.User-Agent: "Mozilla/5.0 (Gobuster)" AND response.status: 401` |
| Hydra brute-force activity | `transaction.remote_address: "10.0.2.15" AND request.headers.User-Agent: "Mozilla/4.0 (Hydra)"` |
| Successful Hydra login evidence | `transaction.remote_address: "10.0.2.15" AND request.headers.User-Agent: "Mozilla/4.0 (Hydra)" AND response.status: 200` |
| Upload activity | `transaction.remote_address: "10.0.2.15" AND http.url: *upload*` |
| Uploaded web shell execution | `transaction.remote_address: "10.0.2.15" AND http.url: /uploads/easy-simple-php-*` |
| LFI and path traversal activity | `transaction.remote_address: "10.0.2.15" AND http.url: *../*` |
| phpMyAdmin activity | `transaction.remote_address: "10.0.2.15" AND http.url: *phpmyadmin*` |

## Investigation lesson

The strongest investigation evidence came from behavior-based queries. For example, the protected admin-login page was better proven through Gobuster activity and a 401 response than by directly searching for the endpoint name.