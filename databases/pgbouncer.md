# PGBouncer [Prometheus exporter for PgBouncer](https://github.com/spreaker/prometheus-pgbouncer-exporter)

## PGBouncer active connectinos    
##### PGBouncer pools are filling up
    
````
      - alert: PgbouncerActiveConnectinos
        expr: pgbouncer_pools_server_active_connections > 200
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "PGBouncer active connectinos (instance {{ $labels.instance }})"
          description: "PGBouncer pools are filling up\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
````

## PGBouncer errors   
##### PGBouncer is logging errors. This may be due to a a server restart or an admin typing commands at the pgbouncer console.
    
````
      - alert: PgbouncerErrors
        expr: increase(pgbouncer_errors_count{errmsg!="server conn crashed?"}[5m]) > 10
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "PGBouncer errors (instance {{ $labels.instance }})"
          description: "PGBouncer is logging errors. This may be due to a a server restart or an admin typing commands at the pgbouncer console.\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
````

## PGBouncer max connections   
##### The number of PGBouncer client connections has reached max_client_conn.
    
````
      - alert: PgbouncerMaxConnections
        expr: rate(pgbouncer_errors_count{errmsg="no more connections allowed (max_client_conn)"}[1m]) > 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "PGBouncer max connections (instance {{ $labels.instance }})"
          description: "The number of PGBouncer client connections has reached max_client_conn.\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
````
