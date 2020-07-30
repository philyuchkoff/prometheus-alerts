## Cassandra

###  [Cassandra Exporter](https://github.com/criteo/cassandra_exporter)

-   #### Cassandra hints count
    
##### Cassandra hints count has changed on {{ $labels.instance }} some nodes may go down
    
```yaml
      - alert: CassandraHintsCount
        expr: changes(cassandra_stats{name="org:apache:cassandra:metrics:storage:totalhints:count"}[1m]) > 3
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Cassandra hints count (instance {{ $labels.instance }})"
          description: "Cassandra hints count has changed on {{ $labels.instance }} some nodes may go down\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Cassandra compaction task pending
    
##### Many Cassandra compaction tasks are pending. You might need to increase I/O capacity by adding nodes to the cluster
    
```yaml
      - alert: CassandraCompactionTaskPending
        expr: avg_over_time(cassandra_stats{name="org:apache:cassandra:metrics:compaction:pendingtasks:value"}[30m]) > 100
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Cassandra compaction task pending (instance {{ $labels.instance }})"
          description: "Many Cassandra compaction tasks are pending. You might need to increase I/O capacity by adding nodes to the cluster.\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Cassandra viewwrite latency
    
##### High viewwrite latency on {{ $labels.instance }} cassandra node
    
```yaml
      - alert: CassandraViewwriteLatency
        expr: cassandra_stats{name="org:apache:cassandra:metrics:clientrequest:viewwrite:viewwritelatency:99thpercentile",service="cas"} > 100000
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Cassandra viewwrite latency (instance {{ $labels.instance }})"
          description: "High viewwrite latency on {{ $labels.instance }} cassandra node\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Cassandra cool hacker
    
##### Increase of Cassandra authentication failures
    
```yaml
      - alert: CassandraCoolHacker
        expr: irate(cassandra_stats{name="org:apache:cassandra:metrics:client:authfailure:count"}[1m]) > 5
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Cassandra cool hacker (instance {{ $labels.instance }})"
          description: "Increase of Cassandra authentication failures\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Cassandra node down
    
##### Cassandra node down
    
```yaml
      - alert: CassandraNodeDown
        expr: sum(cassandra_stats{name="org:apache:cassandra:net:failuredetector:downendpointcount"}) by (service,group,cluster,env) > 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Cassandra node down (instance {{ $labels.instance }})"
          description: "Cassandra node down\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Cassandra commitlog pending tasks
    
##### Unexpected number of Cassandra commitlog pending tasks
    
```yaml
      - alert: CassandraCommitlogPendingTasks
        expr: cassandra_stats{name="org:apache:cassandra:metrics:commitlog:pendingtasks:value"} > 15
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Cassandra commitlog pending tasks (instance {{ $labels.instance }})"
          description: "Unexpected number of Cassandra commitlog pending tasks\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Cassandra compaction executor blocked tasks
    
##### Some Cassandra compaction executor tasks are blocked
    
```yaml
      - alert: CassandraCompactionExecutorBlockedTasks
        expr: cassandra_stats{name="org:apache:cassandra:metrics:threadpools:internal:compactionexecutor:currentlyblockedtasks:count"} > 0
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Cassandra compaction executor blocked tasks (instance {{ $labels.instance }})"
          description: "Some Cassandra compaction executor tasks are blocked\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Cassandra flush writer blocked tasks
    
##### Some Cassandra flush writer tasks are blocked
    
```yaml
      - alert: CassandraFlushWriterBlockedTasks
        expr: cassandra_stats{name="org:apache:cassandra:metrics:threadpools:internal:memtableflushwriter:currentlyblockedtasks:count"} > 0
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Cassandra flush writer blocked tasks (instance {{ $labels.instance }})"
          description: "Some Cassandra flush writer tasks are blocked\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Cassandra repair pending tasks
    
##### Some Cassandra repair tasks are pending
    
```yaml
      - alert: CassandraRepairPendingTasks
        expr: cassandra_stats{name="org:apache:cassandra:metrics:threadpools:internal:antientropystage:pendingtasks:value"} > 2
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Cassandra repair pending tasks (instance {{ $labels.instance }})"
          description: "Some Cassandra repair tasks are pending\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Cassandra repair blocked tasks
    
##### Some Cassandra repair tasks are blocked
    
```yaml
      - alert: CassandraRepairBlockedTasks
        expr: cassandra_stats{name="org:apache:cassandra:metrics:threadpools:internal:antientropystage:currentlyblockedtasks:count"} > 0
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Cassandra repair blocked tasks (instance {{ $labels.instance }})"
          description: "Some Cassandra repair tasks are blocked\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Cassandra connection timeouts total
    
##### Some connection between nodes are ending in timeout
    
```yaml
      - alert: CassandraConnectionTimeoutsTotal
        expr: rate(cassandra_stats{name="org:apache:cassandra:metrics:connection:totaltimeouts:count"}[1m]) > 5
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Cassandra connection timeouts total (instance {{ $labels.instance }})"
          description: "Some connection between nodes are ending in timeout\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Cassandra storage exceptions
    
##### Something is going wrong with cassandra storage
    
```yaml
      - alert: CassandraStorageExceptions
        expr: changes(cassandra_stats{name="org:apache:cassandra:metrics:storage:exceptions:count"}[1m]) > 1
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Cassandra storage exceptions (instance {{ $labels.instance }})"
          description: "Something is going wrong with cassandra storage\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
