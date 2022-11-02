# VMware : [pryorda/vmware_exporter](https://github.com/pryorda/vmware_exporter)

## Virtual Machine Memory Warning
#### High memory usage on {{ $labels.instance }}: {{ $value | printf "%.2f"}}%
````
  - alert: VirtualMachineMemoryWarning
    expr: vmware_vm_mem_usage_average / 100 >= 80 and vmware_vm_mem_usage_average / 100 < 90
    for: 5m
    labels:
      severity: warning
    annotations:
      summary: Virtual Machine Memory Warning (instance {{ $labels.instance }})
      description: "High memory usage on {{ $labels.instance }}: {{ $value | printf \"%.2f\"}}%\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
````

## Virtual Machine Memory Critical
#### High memory usage on {{ $labels.instance }}: {{ $value | printf "%.2f"}}%
````
- alert: VirtualMachineMemoryCritical
    expr: vmware_vm_mem_usage_average / 100 >= 90
    for: 1m
    labels:
      severity: critical
    annotations:
      summary: Virtual Machine Memory Critical (instance {{ $labels.instance }})
      description: "High memory usage on {{ $labels.instance }}: {{ $value | printf \"%.2f\"}}%\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
````

## High Number of Snapshots
#### High snapshots number on {{ $labels.instance }}: {{ $value }}
````
- alert: HighNumberOfSnapshots
    expr: vmware_vm_snapshots > 3
    for: 30m
    labels:
      severity: warning
    annotations:
      summary: High Number of Snapshots (instance {{ $labels.instance }})
      description: "High snapshots number on {{ $labels.instance }}: {{ $value }}\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
````

## Outdated Snapshots
#### Outdated snapshots on {{ $labels.instance }}: {{ $value | printf "%.0f"}} days
````
- alert: OutdatedSnapshots
    expr: (time() - vmware_vm_snapshot_timestamp_seconds) / (60 * 60 * 24) >= 3
    for: 5m
    labels:
      severity: warning
    annotations:
      summary: Outdated Snapshots (instance {{ $labels.instance }})
      description: "Outdated snapshots on {{ $labels.instance }}: {{ $value | printf \"%.0f\"}} days\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
 ````
