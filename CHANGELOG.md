# Changelog

Все заметные изменения в правилах Prometheus отслеживаются в этом файле.
Формат основан на [Keep a Changelog](https://keepachangelog.com/ru/1.1.0/).

## [0.1.0] - 2026-08-03

### Добавлено
- Правила для новых инструментов: Grafana, Alertmanager, Blackbox Exporter, OpenTelemetry Collector, Tempo, Mimir, VictoriaMetrics, ClickHouse, Valkey, DragonflyDB, MSSQL, Memcached, InfluxDB, ArgoCD, Harbor, K3s, containerd, GitLab Runner, GitHub Actions Runner, Windows Exporter, IPMI, Proxmox, KVM/libvirt, Longhorn, Rook, Keycloak, PHP-FPM, Sidekiq, CoreDNS.
- Правила Podman в `container-runtimes/`.
- CI-валидация правил через `promtool check rules` (.github/workflows/validate.yml).

### Изменено
- Все файлы `.md` сконвертированы в `.yml` (готовые для подключения через `rule_files`).
- Директория `some/` реорганизована: правила распределены по смысловым каталогам (`observability/`, `logging/`, `ci-cd/`, `network/`, `virtualization/`, `host/`).
- README обновлён под новую структуру.

### Исправлено
- Удалён дубликат алерта `PrometheusJobMissing`.
- Заменена удалённая метрика `apiserver_request_latencies_bucket` на `apiserver_request_duration_seconds_bucket`.
- Заменена удалённая метрика `container_last_seen` на `container_start_time_seconds`.
- Исправлены отступы YAML в правилах VMware.
- Исправлены дублирующиеся имена групп (`EmbeddedExporter` переименована в уникальные: Loki, Promtail, Thanos, Minio, Linkerd, Nomad, Istio, Etcd).
- Устранены дубликаты алертов в etcd (`EtcdHighNumberOfFailedGrpcRequestsCritical`, `EtcdHighNumberOfFailedHttpRequestsCritical`).
- Исправлен синтаксис выражений: PostgreSQL (`pg_replication_lag_bytes`), HAProxy (subquery), ArgoCD (селекторы меток).

[0.1.0]: https://github.com/philyuchkoff/prometheus-alerts/releases/tag/v0.1.0