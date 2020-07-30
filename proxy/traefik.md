## Traefik

### [Traefik Exporter](https://docs.traefik.io/observability/metrics/prometheus/)

-   #### Traefik backend down
    
##### All Traefik backends are down
    
```yaml
      - alert: TraefikBackendDown
        expr: count(traefik_backend_server_up) by (backend) == 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Traefik backend down (instance {{ $labels.instance }})"
          description: "All Traefik backends are down\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Traefik high HTTP 4xx error rate backend
    
##### Traefik backend 4xx error rate is above 5%
    
```yaml
      - alert: TraefikHighHttp4xxErrorRateBackend
        expr: sum(rate(traefik_backend_requests_total{code=~"4.*"}[3m])) by (backend) / sum(rate(traefik_backend_requests_total[3m])) by (backend) * 100 > 5
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Traefik high HTTP 4xx error rate backend (instance {{ $labels.instance }})"
          description: "Traefik backend 4xx error rate is above 5%\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Traefik high HTTP 5xx error rate backend
    
##### Traefik backend 5xx error rate is above 5%
    
```yaml
      - alert: TraefikHighHttp5xxErrorRateBackend
        expr: sum(rate(traefik_backend_requests_total{code=~"5.*"}[3m])) by (backend) / sum(rate(traefik_backend_requests_total[3m])) by (backend) * 100 > 5
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Traefik high HTTP 5xx error rate backend (instance {{ $labels.instance }})"
          description: "Traefik backend 5xx error rate is above 5%\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
