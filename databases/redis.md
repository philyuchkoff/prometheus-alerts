## Redis

### [Prometheus Redis Metrics Exporter](https://github.com/oliver006/redis_exporter)
-   #### Redis down
    
##### Redis instance is down
```yaml
      - alert: RedisDown
        expr: redis_up == 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Redis down (instance {{ $labels.instance }})"
          description: "Redis instance is down\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Redis missing master
    
##### Redis cluster has no node marked as master
    
```yaml
      - alert: RedisMissingMaster
        expr: count(redis_instance_info{role="master"}) == 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Redis missing master (instance {{ $labels.instance }})"
          description: "Redis cluster has no node marked as master.\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Redis too many masters
    
##### Redis cluster has too many nodes marked as master
    
```yaml
      - alert: RedisTooManyMasters
        expr: count(redis_instance_info{role="master"}) > 1
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Redis too many masters (instance {{ $labels.instance }})"
          description: "Redis cluster has too many nodes marked as master.\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Redis disconnected slaves
    
##### Redis not replicating for all slaves. Consider reviewing the redis replication status
```yaml
      - alert: RedisDisconnectedSlaves
        expr: count without (instance, job) (redis_connected_slaves) - sum without (instance, job) (redis_connected_slaves) - 1 > 1
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Redis disconnected slaves (instance {{ $labels.instance }})"
          description: "Redis not replicating for all slaves. Consider reviewing the redis replication status.\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Redis replication broken
    
##### Redis instance lost a slave
```yaml
      - alert: RedisReplicationBroken
        expr: delta(redis_connected_slaves[1m]) < 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Redis replication broken (instance {{ $labels.instance }})"
          description: "Redis instance lost a slave\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Redis cluster flapping
    
##### Changes have been detected in Redis replica connection. This can occur when replica nodes lose connection to the master and reconnect (a.k.a flapping)
    
```yaml
      - alert: RedisClusterFlapping
        expr: changes(redis_connected_slaves[5m]) > 2
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Redis cluster flapping (instance {{ $labels.instance }})"
          description: "Changes have been detected in Redis replica connection. This can occur when replica nodes lose connection to the master and reconnect (a.k.a flapping).\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Redis missing backup
    
##### Redis has not been backuped for 24 hours
    
```yaml
      - alert: RedisMissingBackup
        expr: time() - redis_rdb_last_save_timestamp_seconds > 60 * 60 * 24
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Redis missing backup (instance {{ $labels.instance }})"
          description: "Redis has not been backuped for 24 hours\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Redis out of memory
    
##### Redis is running out of memory (> 90%)
    
```yaml
      - alert: RedisOutOfMemory
        expr: redis_memory_used_bytes / redis_total_system_memory_bytes * 100 > 90
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Redis out of memory (instance {{ $labels.instance }})"
          description: "Redis is running out of memory (> 90%)\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Redis too many connections
    
##### Redis instance has too many connections
    
```yaml
      - alert: RedisTooManyConnections
        expr: redis_connected_clients > 100
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Redis too many connections (instance {{ $labels.instance }})"
          description: "Redis instance has too many connections\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Redis not enough connections
    
##### Redis instance should have more connections (> 5)
    
```yaml
      - alert: RedisNotEnoughConnections
        expr: redis_connected_clients < 5
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Redis not enough connections (instance {{ $labels.instance }})"
          description: "Redis instance should have more connections (> 5)\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Redis rejected connections
    
##### Some connections to Redis has been rejected
    
```yaml
      - alert: RedisRejectedConnections
        expr: increase(redis_rejected_connections_total[1m]) > 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Redis rejected connections (instance {{ $labels.instance }})"
          description: "Some connections to Redis has been rejected\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
