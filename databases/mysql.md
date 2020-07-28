## MySQL

### [Prometheus MySQL exporter](https://github.com/prometheus/mysqld_exporter)

- #### MySQL down
##### MySQL instance is down on {{ $labels.instance }}

```yaml
 - alert: MysqlDown
    expr: mysql_up == 0
    for: 5m
    labels:
      severity: critical
    annotations:
      summary: "MySQL down (instance {{ $labels.instance }})"
      description: "MySQL instance is down on {{ $labels.instance }}\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
-   #### MySQL too many connections
    
##### More than 80% of MySQL connections are in use on {{ $labels.instance }}
    
```yaml
      - alert: MysqlTooManyConnections
        expr: avg by (instance) (max_over_time(mysql_global_status_threads_connected[5m])) / avg by (instance) (mysql_global_variables_max_connections) * 100 > 80
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "MySQL too many connections (instance {{ $labels.instance }})"
          description: "More than 80% of MySQL connections are in use on {{ $labels.instance }}\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### MySQL high threads running
    
##### More than 60% of MySQL connections are in running state on {{ $labels.instance }}
    
```yaml
      - alert: MysqlHighThreadsRunning
        expr: avg by (instance) (max_over_time(mysql_global_status_threads_running[5m])) / avg by (instance) (mysql_global_variables_max_connections) * 100 > 60
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "MySQL high threads running (instance {{ $labels.instance }})"
          description: "More than 60% of MySQL connections are in running state on {{ $labels.instance }}\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### MySQL Slave IO thread not running
    
##### MySQL Slave IO thread not running on {{ $labels.instance }}
    
```yaml
      - alert: MysqlSlaveIoThreadNotRunning
        expr: mysql_slave_status_master_server_id > 0 and ON (instance) mysql_slave_status_slave_io_running == 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "MySQL Slave IO thread not running (instance {{ $labels.instance }})"
          description: "MySQL Slave IO thread not running on {{ $labels.instance }}\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
        
-   #### MySQL Slave SQL thread not running
    
##### MySQL Slave SQL thread not running on {{ $labels.instance }}
    
```yaml
      - alert: MysqlSlaveSqlThreadNotRunning
        expr: mysql_slave_status_master_server_id > 0 and ON (instance) mysql_slave_status_slave_sql_running == 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "MySQL Slave SQL thread not running (instance {{ $labels.instance }})"
          description: "MySQL Slave SQL thread not running on {{ $labels.instance }}\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### MySQL Slave replication lag
    
##### MysqL replication lag on {{ $labels.instance }}
    
```yaml
      - alert: MysqlSlaveReplicationLag
        expr: mysql_slave_status_master_server_id > 0 and ON (instance) (mysql_slave_status_seconds_behind_master - mysql_slave_status_sql_delay) > 300
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "MySQL Slave replication lag (instance {{ $labels.instance }})"
          description: "MysqL replication lag on {{ $labels.instance }}\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### MySQL slow queries
    
##### MySQL server is having some slow queries.
    
```yaml
      - alert: MysqlSlowQueries
        expr: mysql_global_status_slow_queries > 0
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "MySQL slow queries (instance {{ $labels.instance }})"
          description: "MySQL server is having some slow queries.\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### MySQL restarted
    
##### MySQL has just been restarted, less than one minute ago on {{ $labels.instance }}.
    
```yaml
      - alert: MysqlRestarted
        expr: mysql_global_status_uptime < 60
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "MySQL restarted (instance {{ $labels.instance }})"
          description: "MySQL has just been restarted, less than one minute ago on {{ $labels.instance }}.\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
