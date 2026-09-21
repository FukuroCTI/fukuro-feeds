<!-- fukuro-feeds:readme -->
# fukuro-feeds

Machine-readable threat indicators from Malaysia-focused threat hunting: IP addresses, domains, URLs and file hashes, in STIX 2.1, MISP feed format, CSV and plain lists. TLP:CLEAR: no restriction on sharing.

The written reports are in the companion reports repository. This repository is generated from it, so it is rebuilt in full each time and never edited by hand.

## Files

| Path | What it is |
| --- | --- |
| `stix/bundle.json` | One STIX 2.1 bundle of every indicator that is currently valid, with the reports and ATT&CK techniques behind them |
| `misp/` | A MISP feed (`manifest.json`, `hashes.csv` and one event per case) |
| `iocs.csv` | The same indicators as a table, with first seen, last confirmed and expiry |
| `lists/` | Plain lists, one value per line: `domains.txt`, `urls.txt`, `ips.txt`, `sha256.txt`, `sha1.txt`, `md5.txt` |

## Using it

- **MISP:** Sync Actions, then List Feeds, then Add Feed. Source format "MISP Feed", input source "Network", URL `https://raw.githubusercontent.com/FukuroCTI/fukuro-feeds/main/misp`.
- **OpenCTI or any STIX tool:** import `https://raw.githubusercontent.com/FukuroCTI/fukuro-feeds/main/stix/bundle.json`.
- **Firewalls and scripts:** fetch a file from `https://raw.githubusercontent.com/FukuroCTI/fukuro-feeds/main/lists/`.

## Indicators expire

Indicators go stale: attacker sites are taken down, addresses are reused by innocent sites, and hacked sites are cleaned up. Only indicators that are still within their lifetime are published, counted from when they were last confirmed:

| Indicator | Lifetime |
| --- | --- |
| IP addresses | 14 days |
| URLs | 30 days |
| Domains | 90 days |
| File hashes | does not expire |

Expired indicators drop out on the next update. The STIX bundle carries an explicit `valid_until`, and your platform may apply its own rules on top.

## What is included

- Only indicators from cases judged malicious.
- URLs are published without their query string or fragment, which can carry personal data.
- Reserved and private addresses, whole shared platforms, and official domains of known brands are left out.

## No warranty

Indicators are assessments, not legal findings, and can be wrong. Review before blocking anything important.
