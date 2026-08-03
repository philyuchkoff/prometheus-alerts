
- [Prometheus documentation](https://prometheus.io/docs/introduction/overview/)

Готовые наборы правил Prometheus для разных компонентов. Все файлы `.yml` — валидные правила для подключения через `rule_files`.

### Prometheus
[Prometheus self-monitoring](prometheus.yml)

### Observability
- [Grafana](observability/grafana.yml)
- [Alertmanager](observability/alertmanager.yml)
- [Blackbox Exporter](observability/blackbox.yml)
- [OpenTelemetry Collector](observability/opentelemetry.yml)
- [Tempo](observability/tempo.yml)
- [Mimir](observability/mimir.yml)
- [VictoriaMetrics](observability/victoriametrics.yml)
- [Thanos](observability/thanos.yml)

### Logging
- [Loki](logging/loki.yml)
- [Promtail](logging/promtail.yml)

### Docker Containers
[cAdvisor](docker-containers.yml)

### Container runtimes
- [Podman](container-runtimes/podman.yml)
- [containerd](container-runtimes/containerd.yml)

### Databases

- [MySQL](databases/mysql.yml)
- [PostgreSQL](databases/postgresql.yml)
- [Patroni](databases/patroni.yml)
- [PGBouncer](databases/pgbouncer.yml)
- [Redis](databases/redis.yml)
- [Valkey](databases/valkey.yml)
- [DragonflyDB](databases/dragonfly.yml)
- [MongoDB](databases/mongodb.yml)
- [Cassandra](databases/cassandra.yml)
- [ClickHouse](databases/clickhouse.yml)
- [MSSQL](databases/mssql.yml)
- [Memcached](databases/memcached.yml)
- [InfluxDB](databases/influxdb.yml)

### Brokers

- [RabbitMQ](brokers/rabbitmq.yml)
- [Zookeeper](brokers/zookeeper.yml)
- [Kafka](brokers/kafka.yml)
- [Elasticsearch](brokers/elasticsearch.yml)

### Proxies and load balancers

- [Nginx](proxy/nginx.yml)
- [HAProxy v.2](proxy/haproxy.yml)
- [Traefik](proxy/traefik.yml)

### Runtimes
- [PHP-FPM](runtimes/php-fpm.yml)
- [JVM](runtimes/jvm.yml)
- [Sidekiq](runtimes/sidekiq.yml)

### Orchestrators
- [Kubernetes](orchestrators/k8s.yml)
- [K3s](orchestrators/k3s.yml)
- [Nomad](orchestrators/nomad.yml)
- [Consul](orchestrators/consul.yml)
- [Etcd](orchestrators/etcd.yml)
- [Linkerd](orchestrators/linkerd.yml)
- [Istio](orchestrators/istio.yml)
- [ArgoCD](orchestrators/argocd.yml)
- [Harbor](orchestrators/harbor.yml)

### CI/CD
- [Jenkins](ci-cd/jenkins.yml)
- [GitLab Runner](ci-cd/gitlab-runner.yml)
- [GitHub Runner](ci-cd/github-runner.yml)

### Host monitoring
- [Node Exporter](host/node-exporter.yml)
- [Windows Exporter](host/windows-exporter.yml)
- [IPMI](host/ipmi.yml)

### Virtualization
- [VMware](virtualization/vmware.yml)
- [Proxmox](virtualization/proxmox.yml)
- [KVM/libvirt](virtualization/kvm.yml)

### Network and storage
- [CoreDNS](network/coredns.yml)
- [Ceph](storage/ceph.yml)
- [MinIO](storage/minio.yml)
- [Longhorn](storage/longhorn.yml)
- [Rook](storage/rook.yml)

### Security
- [Keycloak](security/keycloak.yml)
- [SSL/TLS](network/ssltls.yml)

## Как подключить

В `prometheus.yml` добавьте нужные файлы в `rule_files`:

```yaml
rule_files:
  - databases/mysql.yml
  - proxy/haproxy.yml
```

## Релизы

Правила «заморожены» в релизах по версиям. Каждый релиз сопровождается тегом `vX.Y.Z` и описанием в [CHANGELOG.md](CHANGELOG.md). Подключайте пакет правил по тегу для воспроизводимости:

```
https://raw.githubusercontent.com/philyuchkoff/prometheus-alerts/<tag>/databases/mysql.yml
```

Новый релиз создаётся вручную через GitHub Releases или через `git tag vX.Y.Z && git push --tags`.

## CI

Для каждого PR и пуша в `master` запускается проверка всех правил через `promtool check rules` и unit-тесты выражений через `promtool test rules` (см. `.github/workflows/validate.yml`).

## Тесты

Выражения покрыты unit-тестами (формат `promtool test rules`) в каталоге `tests/`:

```
promtool test rules tests/prometheus-test.yml
promtool test rules tests/mysql-test.yml
promtool test rules tests/podman-test.yml
```

Чтобы добиться зелёного CI для нового файла правил, добавьте соответствующий `tests/<name>-test.yml`. 