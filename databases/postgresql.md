## PostgreSQL

### [PostgreSQL Server Exporter](https://github.com/wrouesnel/postgres_exporter/)


-   #### Postgresql instance is down
    

    
```yaml
      - alert: PostgresqlDown
        expr: pg_up == 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Postgresql down (instance {{ $labels.instance }})"
          description: "Postgresql instance is down\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql restarted
    
    
```yaml
      - alert: PostgresqlRestarted
        expr: time() - pg_postmaster_start_time_seconds < 60
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Postgresql restarted (instance {{ $labels.instance }})"
          description: "Postgresql restarted\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql exporter error
    
##### Postgresql exporter is showing errors. A query may be buggy in query.yaml
    
```yaml
      - alert: PostgresqlExporterError
        expr: pg_exporter_last_scrape_error > 0
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Postgresql exporter error (instance {{ $labels.instance }})"
          description: "Postgresql exporter is showing errors. A query may be buggy in query.yaml\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql replication lag
    
##### PostgreSQL replication lag is going up (> 10s)
    
```yaml
      - alert: PostgresqlReplicationLag
        expr: (pg_replication_lag) > 10 and ON(instance) (pg_replication_is_replica == 1)
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Postgresql replication lag (instance {{ $labels.instance }})"
          description: "PostgreSQL replication lag is going up (> 10s)\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql table not vaccumed
    
##### Table has not been vaccum for 24 hours
    
```yaml
      - alert: PostgresqlTableNotVaccumed
        expr: time() - pg_stat_user_tables_last_autovacuum > 60 * 60 * 24
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Postgresql table not vaccumed (instance {{ $labels.instance }})"
          description: "Table has not been vaccum for 24 hours\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql table not analyzed
    
##### Table has not been analyzed for 24 hours
    
```yaml
      - alert: PostgresqlTableNotAnalyzed
        expr: time() - pg_stat_user_tables_last_autoanalyze > 60 * 60 * 24
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Postgresql table not analyzed (instance {{ $labels.instance }})"
          description: "Table has not been analyzed for 24 hours\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql too many connections
    
##### PostgreSQL instance has too many connections
    
```yaml
      - alert: PostgresqlTooManyConnections
        expr: sum by (datname) (pg_stat_activity_count{datname!~"template.*|postgres"}) > pg_settings_max_connections * 0.9
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Postgresql too many connections (instance {{ $labels.instance }})"
          description: "PostgreSQL instance has too many connections\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql not enough connections
    
##### PostgreSQL instance should have more connections (> 5)
    
```yaml
      - alert: PostgresqlNotEnoughConnections
        expr: sum by (datname) (pg_stat_activity_count{datname!~"template.*|postgres"}) < 5
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Postgresql not enough connections (instance {{ $labels.instance }})"
          description: "PostgreSQL instance should have more connections (> 5)\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql dead locks
    
##### PostgreSQL has dead-locks
    
```yaml
      - alert: PostgresqlDeadLocks
        expr: rate(pg_stat_database_deadlocks{datname!~"template.*|postgres"}[1m]) > 0
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Postgresql dead locks (instance {{ $labels.instance }})"
          description: "PostgreSQL has dead-locks\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql slow queries
    
##### PostgreSQL executes slow queries
    
```yaml
      - alert: PostgresqlSlowQueries
        expr: pg_slow_queries > 0
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Postgresql slow queries (instance {{ $labels.instance }})"
          description: "PostgreSQL executes slow queries\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql high rollback rate
    
##### Ratio of transactions being aborted compared to committed is > 2 %
    
```yaml
      - alert: PostgresqlHighRollbackRate
        expr: rate(pg_stat_database_xact_rollback{datname!~"template.*"}[3m]) / rate(pg_stat_database_xact_commit{datname!~"template.*"}[3m]) > 0.02
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Postgresql high rollback rate (instance {{ $labels.instance }})"
          description: "Ratio of transactions being aborted compared to committed is > 2 %\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql commit rate low
    
##### Postgres seems to be processing very few transactions
    
```yaml
      - alert: PostgresqlCommitRateLow
        expr: rate(pg_stat_database_xact_commit[1m]) < 10
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Postgresql commit rate low (instance {{ $labels.instance }})"
          description: "Postgres seems to be processing very few transactions\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql low XID consumption
    
##### Postgresql seems to be consuming transaction IDs very slowly
    
```yaml
      - alert: PostgresqlLowXidConsumption
        expr: rate(pg_txid_current[1m]) < 5
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Postgresql low XID consumption (instance {{ $labels.instance }})"
          description: "Postgresql seems to be consuming transaction IDs very slowly\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresqllow XLOG consumption
    
##### Postgres seems to be consuming XLOG very slowly
    
```yaml
      - alert: PostgresqllowXlogConsumption
        expr: rate(pg_xlog_position_bytes[1m]) < 100
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Postgresqllow XLOG consumption (instance {{ $labels.instance }})"
          description: "Postgres seems to be consuming XLOG very slowly\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql WALE replication stopped
    
##### WAL-E replication seems to be stopped
    
```yaml
      - alert: PostgresqlWaleReplicationStopped
        expr: rate(pg_xlog_position_bytes[1m]) == 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Postgresql WALE replication stopped (instance {{ $labels.instance }})"
          description: "WAL-E replication seems to be stopped\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql high rate statement timeout
    
##### Postgres transactions showing high rate of statement timeouts
    
```yaml
      - alert: PostgresqlHighRateStatementTimeout
        expr: rate(postgresql_errors_total{type="statement_timeout"}[5m]) > 3
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Postgresql high rate statement timeout (instance {{ $labels.instance }})"
          description: "Postgres transactions showing high rate of statement timeouts\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql high rate deadlock
    
##### Postgres detected deadlocks
    
```yaml
      - alert: PostgresqlHighRateDeadlock
        expr: rate(postgresql_errors_total{type="deadlock_detected"}[1m]) * 60 > 1
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Postgresql high rate deadlock (instance {{ $labels.instance }})"
          description: "Postgres detected deadlocks\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql replication lab bytes
    
##### Postgres Replication lag (in bytes) is high
    
```yaml
      - alert: PostgresqlReplicationLabBytes
        expr: (pg_xlog_position_bytes and pg_replication_is_replica == 0) - GROUP_RIGHT(instance) (pg_xlog_position_bytes and pg_replication_is_replica == 1) > 1e+09
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Postgresql replication lab bytes (instance {{ $labels.instance }})"
          description: "Postgres Replication lag (in bytes) is high\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql unused replication slot
    
##### Unused Replication Slots
    
```yaml
      - alert: PostgresqlUnusedReplicationSlot
        expr: pg_replication_slots_active == 0
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Postgresql unused replication slot (instance {{ $labels.instance }})"
          description: "Unused Replication Slots\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql too many dead tuples
    
##### PostgreSQL dead tuples is too large
    
```yaml
      - alert: PostgresqlTooManyDeadTuples
        expr: ((pg_stat_user_tables_n_dead_tup > 10000) / (pg_stat_user_tables_n_live_tup + pg_stat_user_tables_n_dead_tup)) >= 0.1 unless ON(instance) (pg_replication_is_replica == 1)
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Postgresql too many dead tuples (instance {{ $labels.instance }})"
          description: "PostgreSQL dead tuples is too large\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql split brain
    
##### Split Brain, too many primary Postgresql databases in read-write mode
    
```yaml
      - alert: PostgresqlSplitBrain
        expr: count(pg_replication_is_replica == 0) != 1
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Postgresql split brain (instance {{ $labels.instance }})"
          description: "Split Brain, too many primary Postgresql databases in read-write mode\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql promoted node
    
##### Postgresql standby server has been promoted as primary node
    
```yaml
      - alert: PostgresqlPromotedNode
        expr: pg_replication_is_replica and changes(pg_replication_is_replica[1m]) > 0
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Postgresql promoted node (instance {{ $labels.instance }})"
          description: "Postgresql standby server has been promoted as primary node\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql configuration changed
    
##### Postgres Database configuration change has occurred
    
```yaml
      - alert: PostgresqlConfigurationChanged
        expr: {__name__=~"pg_settings_.*"} != ON(__name__) {__name__=~"pg_settings_([^t]|t[^r]|tr[^a]|tra[^n]|tran[^s]|trans[^a]|transa[^c]|transac[^t]|transact[^i]|transacti[^o]|transactio[^n]|transaction[^_]|transaction_[^r]|transaction_r[^e]|transaction_re[^a]|transaction_rea[^d]|transaction_read[^_]|transaction_read_[^o]|transaction_read_o[^n]|transaction_read_on[^l]|transaction_read_onl[^y]).*"} OFFSET 5m
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Postgresql configuration changed (instance {{ $labels.instance }})"
          description: "Postgres Database configuration change has occurred\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql SSL compression active
    
##### Database connections with SSL compression enabled. This may add significant jitter in replication delay. Replicas should turn off SSL compression via `sslcompression=0` in `recovery.conf`
    
```yaml
      - alert: PostgresqlSslCompressionActive
        expr: sum(pg_stat_ssl_compression) > 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Postgresql SSL compression active (instance {{ $labels.instance }})"
          description: "Database connections with SSL compression enabled. This may add significant jitter in replication delay. Replicas should turn off SSL compression via `sslcompression=0` in `recovery.conf`.\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Postgresql too many locks acquired
    
##### Too many locks acquired on the database. If this alert happens frequently, we may need to increase the postgres setting max_locks_per_transaction.
    
```yaml
      - alert: PostgresqlTooManyLocksAcquired
        expr: ((sum (pg_locks_count)) / (pg_settings_max_locks_per_transaction * pg_settings_max_connections)) > 0.20
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Postgresql too many locks acquired (instance {{ $labels.instance }})"
          description: "Too many locks acquired on the database. If this alert happens frequently, we may need to increase the postgres setting max_locks_per_transaction.\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
