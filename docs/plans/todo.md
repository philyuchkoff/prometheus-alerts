# TODO

## Высокий приоритет

- [x] Исправить дубль алерта `PrometheusJobMissing` в `prometheus.md`
- [x] Заменить устаревшую метрику `apiserver_request_latencies_bucket` на `apiserver_request_duration_seconds_bucket` в `orchestrators/k8s.yml`
- [x] Заменить удалённую метрику `container_last_seen` на `container_start_time_seconds` в `docker-containers.md`
- [x] Исправить отступы YAML в `some/vmware.md` (алерты вне блока rules)

## Средний приоритет

- [ ] Улучшить правило `KubernetesVolumeFullInFourDays` (predict_linear) в `orchestrators/k8s.yml`
- [x] Добавить `.gitignore`
- [x] Добавить ссылку на Ceph в README (остальные — ZFS, OpenEBS, Juniper, CoreDNS, PHP-FPM, Sidekiq, VictoriaMetrics — без файлов, оставлено на будущее)
- [ ] Уникальные имена групп правил вместо `EmbeddedExporter` (thanos, loki, jenkins и др.)

## Низкий приоритет

- [ ] Добавить LICENSE
- [ ] Добавить CI-проверку правил promtool (.github/workflows)
- [ ] Примеры конфигов prometheus.yml + alertmanager.yml

## История

- _(пусто)_
