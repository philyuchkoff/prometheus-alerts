### [Exporter](https://istio.io/latest/docs/tasks/observability/metrics/querying-metrics/)

````
- name: Istio
  rules:
  - alert: IstioKubernetesGatewayAvailabilityDrop
    expr: min(kube_deployment_status_replicas_available{deployment="istio-ingressgateway", namespace="istio-system"}) without (instance, pod) < 2
    for: 1m
    labels:
      severity: warning
    annotations:
      summary: "Istio Kubernetes gateway availability drop (instance {{ $labels.instance }})"
      description: "Gateway pods have dropped. Inbound traffic will likely be affected.\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"

  - alert: IstioPilotHighTotalRequestRate
    expr: sum(rate(pilot_xds_push_errors[1m])) / sum(rate(pilot_xds_pushes[1m])) * 100 > 5
    for: 1m
    labels:
      severity: warning
    annotations:
      summary: "Istio Pilot high total request rate (instance {{ $labels.instance }})"
      description: "Number of Istio Pilot push errors is too high (> 5%). Envoy sidecars might have outdated configuration.\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"

  - alert: IstioMixerPrometheusDispatchesLow
    expr: sum(rate(mixer_runtime_dispatches_total{adapter=~"prometheus"}[1m])) < 180
    for: 1m
    labels:
      severity: warning
    annotations:
      summary: "Istio Mixer Prometheus dispatches low (instance {{ $labels.instance }})"
      description: "Number of Mixer dispatches to Prometheus is too low. Istio metrics might not be being exported properly.\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"

  - alert: IstioHighTotalRequestRate
    expr: sum(rate(istio_requests_total{reporter="destination"}[5m])) > 1000
    for: 2m
    labels:
      severity: warning
    annotations:
      summary: "Istio high total request rate (instance {{ $labels.instance }})"
      description: "Global request rate in the service mesh is unusually high.\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"

  - alert: IstioLowTotalRequestRate
    expr: sum(rate(istio_requests_total{reporter="destination"}[5m])) < 100
    for: 2m
    labels:
      severity: warning
    annotations:
      summary: "Istio low total request rate (instance {{ $labels.instance }})"
      description: "Global request rate in the service mesh is unusually low.\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"

  - alert: IstioHigh4xxErrorRate
    expr: sum(rate(istio_requests_total{reporter="destination", response_code=~"4.*"}[5m])) / sum(rate(istio_requests_total{reporter="destination"}[5m])) * 100 > 5
    for: 1m
    labels:
      severity: warning
    annotations:
      summary: "Istio high 4xx error rate (instance {{ $labels.instance }})"
      description: "High percentage of HTTP 5xx responses in Istio (> 5%).\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"

  - alert: IstioHigh5xxErrorRate
    expr: sum(rate(istio_requests_total{reporter="destination", response_code=~"5.*"}[5m])) / sum(rate(istio_requests_total{reporter="destination"}[5m])) * 100 > 5
    for: 1m
    labels:
      severity: warning
    annotations:
      summary: "Istio high 5xx error rate (instance {{ $labels.instance }})"
      description: "High percentage of HTTP 5xx responses in Istio (> 5%).\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"

  - alert: IstioHighRequestLatency
    expr: rate(istio_request_duration_milliseconds_sum[1m]) / rate(istio_request_duration_milliseconds_count[1m]) > 0.1
    for: 1m
    labels:
      severity: warning
    annotations:
      summary: "Istio high request latency (instance {{ $labels.instance }})"
      description: "Istio average requests execution is longer than 100ms.\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"

  - alert: IstioLatency99Percentile
    expr: histogram_quantile(0.99, rate(istio_request_duration_milliseconds_bucket[1m])) > 1
    for: 1m
    labels:
      severity: warning
    annotations:
      summary: "Istio latency 99 percentile (instance {{ $labels.instance }})"
      description: "Istio 1% slowest resquests are longer than 1s.\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
````
