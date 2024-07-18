Embedded exporter https://docs.ceph.com/en/quincy/mgr/prometheus/

### Ceph State
#### Ceph instance unhealthy
```yaml
  - alert: CephState
    expr: ceph_health_status != 0
    for: 0m
    labels:
      severity: critical
    annotations:
      summary: Ceph State (instance {{ $labels.instance }})
      description: "Ceph instance unhealthy\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```

### Ceph monitor clock skew
#### Ceph monitor clock skew detected. Please check ntp and hardware clock settings[copy]
```yaml
  - alert: CephMonitorClockSkew
    expr: abs(ceph_monitor_clock_skew_seconds) > 0.2
    for: 2m
    labels:
      severity: warning
    annotations:
      summary: Ceph monitor clock skew (instance {{ $labels.instance }})
      description: "Ceph monitor clock skew detected. Please check ntp and hardware clock settings\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```
### Ceph monitor low space
#### Ceph monitor storage is low.[copy]
```yaml
  - alert: CephMonitorLowSpace
    expr: ceph_monitor_avail_percent < 10
    for: 2m
    labels:
      severity: warning
    annotations:
      summary: Ceph monitor low space (instance {{ $labels.instance }})
      description: "Ceph monitor storage is low.\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```
### Ceph OSD Down
#### Ceph Object Storage Daemon Down[copy]
```yaml
  - alert: CephOsdDown
    expr: ceph_osd_up == 0
    for: 0m
    labels:
      severity: critical
    annotations:
      summary: Ceph OSD Down (instance {{ $labels.instance }})
      description: "Ceph Object Storage Daemon Down\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```
### Ceph high OSD latency
#### Ceph Object Storage Daemon latency is high. Please check if it doesn't stuck in weird state.[copy]
```yaml
  - alert: CephHighOsdLatency
    expr: ceph_osd_perf_apply_latency_seconds > 5
    for: 1m
    labels:
      severity: warning
    annotations:
      summary: Ceph high OSD latency (instance {{ $labels.instance }})
      description: "Ceph Object Storage Daemon latency is high. Please check if it doesn't stuck in weird state.\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```
### Ceph OSD low space
#### Ceph Object Storage Daemon is going out of space. Please add more disks.[copy]
```yaml
  - alert: CephOsdLowSpace
    expr: ceph_osd_utilization > 90
    for: 2m
    labels:
      severity: warning
    annotations:
      summary: Ceph OSD low space (instance {{ $labels.instance }})
      description: "Ceph Object Storage Daemon is going out of space. Please add more disks.\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```
### Ceph OSD reweighted
#### Ceph Object Storage Daemon takes too much time to resize.[copy]
```yaml
  - alert: CephOsdReweighted
    expr: ceph_osd_weight < 1
    for: 2m
    labels:
      severity: warning
    annotations:
      summary: Ceph OSD reweighted (instance {{ $labels.instance }})
      description: "Ceph Object Storage Daemon takes too much time to resize.\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```
### Ceph PG down
#### Some Ceph placement groups are down. Please ensure that all the data are available.[copy]
```yaml
  - alert: CephPgDown
    expr: ceph_pg_down > 0
    for: 0m
    labels:
      severity: critical
    annotations:
      summary: Ceph PG down (instance {{ $labels.instance }})
      description: "Some Ceph placement groups are down. Please ensure that all the data are available.\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```
### Ceph PG incomplete
#### Some Ceph placement groups are incomplete. Please ensure that all the data are available.[copy]
```yaml
  - alert: CephPgIncomplete
    expr: ceph_pg_incomplete > 0
    for: 0m
    labels:
      severity: critical
    annotations:
      summary: Ceph PG incomplete (instance {{ $labels.instance }})
      description: "Some Ceph placement groups are incomplete. Please ensure that all the data are available.\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```
### Ceph PG inconsistent
#### Some Ceph placement groups are inconsistent. Data is available but inconsistent across nodes.[copy]
```yaml
  - alert: CephPgInconsistent
    expr: ceph_pg_inconsistent > 0
    for: 0m
    labels:
      severity: warning
    annotations:
      summary: Ceph PG inconsistent (instance {{ $labels.instance }})
      description: "Some Ceph placement groups are inconsistent. Data is available but inconsistent across nodes.\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```
### Ceph PG activation long
#### Some Ceph placement groups are too long to activate.[copy]
```yaml
  - alert: CephPgActivationLong
    expr: ceph_pg_activating > 0
    for: 2m
    labels:
      severity: warning
    annotations:
      summary: Ceph PG activation long (instance {{ $labels.instance }})
      description: "Some Ceph placement groups are too long to activate.\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```
### Ceph PG backfill full
#### Some Ceph placement groups are located on full Object Storage Daemon on cluster. Those PGs can be unavailable shortly. Please check OSDs, change weight or reconfigure CRUSH rules.[copy]
```yaml
  - alert: CephPgBackfillFull
    expr: ceph_pg_backfill_toofull > 0
    for: 2m
    labels:
      severity: warning
    annotations:
      summary: Ceph PG backfill full (instance {{ $labels.instance }})
      description: "Some Ceph placement groups are located on full Object Storage Daemon on cluster. Those PGs can be unavailable shortly. Please check OSDs, change weight or reconfigure CRUSH rules.\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```
### Ceph PG unavailable
#### Some Ceph placement groups are unavailable.[copy]
```yaml
  - alert: CephPgUnavailable
    expr: ceph_pg_total - ceph_pg_active > 0
    for: 0m
    labels:
      severity: critical
    annotations:
      summary: Ceph PG unavailable (instance {{ $labels.instance }})
      description: "Some Ceph placement groups are unavailable.\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```
