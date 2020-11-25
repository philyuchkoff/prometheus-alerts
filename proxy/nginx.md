## Nginx

### [Prometheus metric library for Nginx](https://github.com/knyar/nginx-lua-prometheus)

-   #### Nginx high HTTP 4xx error rate
    
##### Too many HTTP requests with status 4xx (> 5%)
    
```yaml
  - alert: NginxHighHttp4xxErrorRate
    expr: sum(rate(nginx_http_requests_total{status=~"^4.."}[1m])) / sum(rate(nginx_http_requests_total[1m])) * 100 > 5
    for: 5m
    labels:
      severity: critical
    annotations:
      summary: Nginx high HTTP 4xx error rate (instance {{ $labels.instance }})
      description: Too many HTTP requests with status 4xx (> 5%)\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}
```
    
-   #### Nginx high HTTP 5xx error rate
    
##### Too many HTTP requests with status 5xx (> 5%)
    
```yaml
  - alert: NginxHighHttp5xxErrorRate
    expr: sum(rate(nginx_http_requests_total{status=~"^5.."}[1m])) / sum(rate(nginx_http_requests_total[1m])) * 100 > 5
    for: 5m
    labels:
      severity: critical
    annotations:
      summary: Nginx high HTTP 5xx error rate (instance {{ $labels.instance }})
      description: Too many HTTP requests with status 5xx (> 5%)\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}
```      
    
-   #### Nginx latency high
    
##### Nginx p99 latency is higher than 10 seconds
    
```yaml
  - alert: NginxLatencyHigh
    expr: histogram_quantile(0.99, sum(rate(nginx_http_request_duration_seconds_bucket[30m])) by (host, node)) > 10
    for: 5m
    labels:
      severity: warning
    annotations:
      summary: Nginx latency high (instance {{ $labels.instance }})
      description: Nginx p99 latency is higher than 10 seconds\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}
```
