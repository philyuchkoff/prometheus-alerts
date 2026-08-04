> **788+ production-ready Prometheus alerting rules for 80+ services — just copy-paste YAML**

- [Русская версия](README-RU.md)

Ready-to-use Prometheus alert rules for various components. All `.yml` files are valid rules to include via `rule_files`.

### Prometheus
[Prometheus self-monitoring](observability/prometheus.yml)

### Observability
- [Grafana](observability/grafana.yml)
- [Alertmanager](observability/alertmanager.yml)
- [Blackbox Exporter](observability/blackbox.yml)
- [OpenTelemetry Collector](observability/opentelemetry.yml)
- [Tempo](observability/tempo.yml)
- [Mimir](observability/mimir.yml)
- [VictoriaMetrics](observability/victoriametrics.yml)
- [Thanos](observability/thanos.yml)
- [Cortex](observability/cortex.yml)
- [Jaeger](observability/jaeger.yml)
- [Grafana Alloy](observability/grafana-alloy.yml)

### Logging
- [Loki](logging/loki.yml)
- [Promtail](logging/promtail.yml)

### Docker Containers
[cAdvisor](container-runtimes/docker-containers.yml)

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
- [OpenSearch](databases/opensearch.yml)
- [Solr](databases/solr.yml)
- [Meilisearch](databases/meilisearch.yml)
- [CouchDB](databases/couchdb.yml)
- [Oracle](databases/oracle.yml)

### Brokers

- [RabbitMQ](brokers/rabbitmq.yml)
- [Zookeeper](brokers/zookeeper.yml)
- [Kafka](brokers/kafka.yml)
- [Elasticsearch](brokers/elasticsearch.yml)
- [NATS](brokers/nats.yml)

### Proxies and load balancers

- [Nginx](proxy/nginx.yml)
- [HAProxy v.2](proxy/haproxy.yml)
- [Traefik](proxy/traefik.yml)
- [Apache](proxy/apache.yml)
- [Caddy](proxy/caddy.yml)
- [Envoy](proxy/envoy.yml)

### Runtimes
- [PHP-FPM](runtimes/php-fpm.yml)
- [JVM](runtimes/jvm.yml)
- [Sidekiq](runtimes/sidekiq.yml)

### Data engineering
- [Apache Flink](runtimes/flink.yml)
- [Apache Spark](runtimes/spark.yml)
- [Apache Hadoop](runtimes/hadoop.yml)

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
- [FluxCD](orchestrators/fluxcd.yml)
- [OpenStack](orchestrators/openstack.yml)
- [OpenEBS](orchestrators/openebs.yml)

### CI/CD
- [Jenkins](ci-cd/jenkins.yml)
- [GitLab CI](ci-cd/gitlab-ci.yml)
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

### Network and security
- [CoreDNS](network/coredns.yml)
- [cert-manager](network/cert-manager.yml)
- [Cilium](network/cilium.yml)
- [WireGuard](network/wireguard.yml)
- [Hashicorp Vault](network/hashicorp-vault.yml)
- [Cloudflare](network/cloudflare.yml)
- [SNMP](network/snmp.yml)
- [Juniper](network/juniper.yml)
- [SpeedTest](network/speedtest.yml)
- [SSL/TLS](network/ssltls.yml)

### Storage
- [Ceph](storage/ceph.yml)
- [MinIO](storage/minio.yml)
- [Longhorn](storage/longhorn.yml)
- [Rook](storage/rook.yml)

### Security
- [Keycloak](security/keycloak.yml)

## How to use

Add the rules you need to `rule_files` in the Prometheus config:

```yaml
rule_files:
  - databases/mysql.yml
  - proxy/haproxy.yml
```

## Releases

Rules are frozen into versioned releases. Each release is tagged `vX.Y.Z` and described in [CHANGELOG.md](CHANGELOG.md). Pin rules to a tag for reproducibility:

```
https://raw.githubusercontent.com/philyuchkoff/prometheus-alerts/<tag>/databases/mysql.yml
```

Create a new release manually via GitHub Releases or via `git tag vX.Y.Z && git push --tags`.

## CI

Every PR and push to `master` runs `promtool check rules` against all rule files and `promtool test rules` for unit tests (see `.github/workflows/validate.yml`).

## Tests

Expressions are covered by unit tests (`promtool test rules` format) in the `tests/` directory:

```
promtool test rules tests/prometheus-test.yml
promtool test rules tests/mysql-test.yml
promtool test rules tests/podman-test.yml
```

To keep CI green for a new rules file, add a matching `tests/<name>-test.yml`.

## Attribution

Part of the rules are adapted from [samber/awesome-prometheus-alerts](https://github.com/samber/awesome-prometheus-alerts) (CC BY 4.0):

- [cert-manager](network/cert-manager.yml)
- [Cilium](network/cilium.yml)
- [WireGuard](network/wireguard.yml)
- [Hashicorp Vault](network/hashicorp-vault.yml)
- [Cloudflare](network/cloudflare.yml)
- [SNMP](network/snmp.yml)
- [Juniper](network/juniper.yml)
- [SpeedTest](network/speedtest.yml)
- [NATS](brokers/nats.yml)
- [OpenSearch](databases/opensearch.yml)
- [Solr](databases/solr.yml)
- [Meilisearch](databases/meilisearch.yml)
- [CouchDB](databases/couchdb.yml)
- [Oracle](databases/oracle.yml)
- [Apache](proxy/apache.yml)
- [Caddy](proxy/caddy.yml)
- [Envoy](proxy/envoy.yml)
- [Apache Flink](runtimes/flink.yml)
- [Apache Spark](runtimes/spark.yml)
- [Apache Hadoop](runtimes/hadoop.yml)
- [Cortex](observability/cortex.yml)
- [Jaeger](observability/jaeger.yml)
- [Grafana Alloy](observability/grafana-alloy.yml)
- [FluxCD](orchestrators/fluxcd.yml)
- [OpenStack](orchestrators/openstack.yml)
- [OpenEBS](orchestrators/openebs.yml)
- [Nomad exporter](orchestrators/nomad.yml)
- [GitLab CI](ci-cd/gitlab-ci.yml)
- [Mimir](observability/mimir.yml)
- [Thanos](observability/thanos.yml)
- [HAProxy](proxy/haproxy.yml)
- [Cassandra](databases/cassandra.yml)
- [ClickHouse](databases/clickhouse.yml)
- [IPMI](host/ipmi.yml)

Each of these files also carries an attribution header pointing to the original source.

## License

Licensed under the [Creative Commons Attribution 4.0 International](LICENSE) (CC BY 4.0).
