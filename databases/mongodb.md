## MongoDB

###  [MongoDB Exporter](https://github.com/dcu/mongodb_exporter)

-   #### MongoDB replication lag
    
##### Mongodb replication lag is more than 10s
    
```yaml
      - alert: MongodbReplicationLag
        expr: avg(mongodb_replset_member_optime_date{state="PRIMARY"}) - avg(mongodb_replset_member_optime_date{state="SECONDARY"}) > 10
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "MongoDB replication lag (instance {{ $labels.instance }})"
          description: "Mongodb replication lag is more than 10s\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### MongoDB replication headroom
    
##### MongoDB replication headroom is <= 0
    
```yaml
      - alert: MongodbReplicationHeadroom
        expr: (avg(mongodb_replset_oplog_tail_timestamp - mongodb_replset_oplog_head_timestamp) - (avg(mongodb_replset_member_optime_date{state="PRIMARY"}) - avg(mongodb_replset_member_optime_date{state="SECONDARY"}))) <= 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "MongoDB replication headroom (instance {{ $labels.instance }})"
          description: "MongoDB replication headroom is <= 0\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### MongoDB replication Status 3
    
##### MongoDB Replication set member either perform startup self-checks, or transition from completing a rollback or resync
    
```yaml
      - alert: MongodbReplicationStatus3
        expr: mongodb_replset_member_state == 3
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "MongoDB replication Status 3 (instance {{ $labels.instance }})"
          description: "MongoDB Replication set member either perform startup self-checks, or transition from completing a rollback or resync\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### MongoDB replication Status 6
    
##### MongoDB Replication set member as seen from another member of the set, is not yet known
    
```yaml
      - alert: MongodbReplicationStatus6
        expr: mongodb_replset_member_state == 6
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "MongoDB replication Status 6 (instance {{ $labels.instance }})"
          description: "MongoDB Replication set member as seen from another member of the set, is not yet known\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### MongoDB replication Status 8
    
##### MongoDB Replication set member as seen from another member of the set, is unreachable
```yaml
      - alert: MongodbReplicationStatus8
        expr: mongodb_replset_member_state == 8
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "MongoDB replication Status 8 (instance {{ $labels.instance }})"
          description: "MongoDB Replication set member as seen from another member of the set, is unreachable\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### MongoDB replication Status 9
    
##### MongoDB Replication set member is actively performing a rollback. Data is not available for reads

```yaml
      - alert: MongodbReplicationStatus9
        expr: mongodb_replset_member_state == 9
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "MongoDB replication Status 9 (instance {{ $labels.instance }})"
          description: "MongoDB Replication set member is actively performing a rollback. Data is not available for reads\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### MongoDB replication Status 10
    
##### MongoDB Replication set member was once in a replica set but was subsequently removed

```yaml
      - alert: MongodbReplicationStatus10
        expr: mongodb_replset_member_state == 10
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "MongoDB replication Status 10 (instance {{ $labels.instance }})"
          description: "MongoDB Replication set member was once in a replica set but was subsequently removed\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### MongoDB number cursors open
    
##### Too many cursors opened by MongoDB for clients (> 10k)
    
```yaml
      - alert: MongodbNumberCursorsOpen
        expr: mongodb_metrics_cursor_open{state="total_open"} > 10000
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "MongoDB number cursors open (instance {{ $labels.instance }})"
          description: "Too many cursors opened by MongoDB for clients (> 10k)\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### MongoDB cursors timeouts
    
##### Too many cursors are timing out
    
```yaml
      - alert: MongodbCursorsTimeouts
        expr: increase(mongodb_metrics_cursor_timed_out_total[10m]) > 100
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "MongoDB cursors timeouts (instance {{ $labels.instance }})"
          description: "Too many cursors are timing out\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### MongoDB too many connections
    
##### Too many connections
    
```yaml
      - alert: MongodbTooManyConnections
        expr: mongodb_connections{state="current"} > 500
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "MongoDB too many connections (instance {{ $labels.instance }})"
          description: "Too many connections\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### MongoDB virtual memory usage
    
##### High memory usage
    
```yaml
      - alert: MongodbVirtualMemoryUsage
        expr: (sum(mongodb_memory{type="virtual"}) BY (ip) / sum(mongodb_memory{type="mapped"}) BY (ip)) > 3
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "MongoDB virtual memory usage (instance {{ $labels.instance }})"
          description: "High memory usage\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
