# Apex SOC Connectors

Read-only client libraries for SIEM and SOC platforms. Extracted from
[Data Center Commander](https://github.com/AAH20/data-center-commander), where these
connectors had no route reaching them — they are a SOC concern, not a data-center
lifecycle one.

**Status:** connector clients only. No server, no agent, no ingestion daemon. Each
module wraps one vendor's API and returns normalised dataclasses.

| Module | Platform | LOC |
|---|---|---|
| `wazuh` | Wazuh (alerts, rules, dashboards) | 4,208 |
| `qradar` | IBM QRadar | 3,850 |
| `chronicle` | Google Chronicle / SecOps | 3,111 |
| `graylog` | Graylog | 2,150 |
| `ossec` | OSSEC | 1,802 |
| `opensearch` | OpenSearch Security Analytics | 1,656 |
| `integration` | Cross-platform glue | 1,663 |
| `metron` | Apache Metron (CEF/HTTP/NetFlow/Syslog parsers) | 1,217 |
| `splunk` | Splunk | 1,132 |

## Install

```bash
pip install -e ".[test]"
```

The `kafka` extra is only needed for the Metron Kafka producers; without it those
connectors import `KafkaProducer = None` and the rest of the package works normally.

## Test

```bash
pytest
```

## Coverage

239 test functions. Four connectors carry colocated suites inside the package
(`src/apex_soc/<vendor>/tests/`) and were never collected in the host project because
its pytest `testpaths` pointed only at the top-level `tests/` directory. They are
collected here.

| Connector | Tests |
|---|---|
| `wazuh` | 67 |
| `graylog` | 56 |
| `chronicle` | 54 |
| `opensearch` | 44 |
| `ossec` | 18 |
| **No tests** | `qradar`, `splunk`, `metron`, `integration` |

The four without tests are the state they arrived in, stated plainly rather than
implied.

## License

AGPL-3.0-only. See `LICENSE`.
