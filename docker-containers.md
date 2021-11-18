## cAdvisor
### [google/cAdvisor](https://github.com/google/cadvisor) 

````
- name: Containers
  rules:
  ````

#### Container killed
A container has disappeared

```yaml
# Если инфраструктура динамическая - часто и много контейнеров запускается, останавливается или перезапускается - может быть много ложных алертов
  - alert: ContainerKilled
    expr: time() - container_last_seen > 60
    for: 0m
    labels:
      severity: warning
    annotations:
      summary: Container killed (instance {{ $labels.instance }})
      description: "A container has disappeared\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```

#### Container absent
A container is absent for 5 min
```yaml
# Если инфраструктура динамическая - часто и много контейнеров запускается, останавливается или перезапускается - может быть много ложных алертов
  - alert: ContainerAbsent
    expr: absent(container_last_seen)
    for: 5m
    labels:
      severity: warning
    annotations:
      summary: Container absent (instance {{ $labels.instance }})
      description: "A container is absent for 5 min\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```
#### Container CPU usage
Container CPU usage is above 80%
```yaml
# cAdvisor иногда жрет много CPU и этот алерт бутет срабатывать часто.
# Чтобы исключить срабатывание алерта по этой причине - нужно исключить серию с пустым именем: container_cpu_usage_seconds_total{name!=""}
  - alert: ContainerCpuUsage
    expr: (sum(rate(container_cpu_usage_seconds_total[3m])) BY (instance, name) * 100) > 80
    for: 2m
    labels:
      severity: warning
    annotations:
      summary: Container CPU usage (instance {{ $labels.instance }})
      description: "Container CPU usage is above 80%\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```
#### Container Memory usage
Container Memory usage is above 80%
```yaml
# Прочитай "How much is too much? The Linux OOMKiller and “used” memory" 
# https://medium.com/faun/how-much-is-too-much-the-linux-oomkiller-and-used-memory-d32186f29c9d
  - alert: ContainerMemoryUsage
    expr: (sum(container_memory_working_set_bytes) BY (instance, name) / sum(container_spec_memory_limit_bytes > 0) BY (instance, name) * 100) > 80
    for: 2m
    labels:
      severity: warning
    annotations:
      summary: Container Memory usage (instance {{ $labels.instance }})
      description: "Container Memory usage is above 80%\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```
#### Container Volume usage
Container Volume usage is above 80%
```yaml
  - alert: ContainerVolumeUsage
    expr: (1 - (sum(container_fs_inodes_free) BY (instance) / sum(container_fs_inodes_total) BY (instance))) * 100 > 80
    for: 2m
    labels:
      severity: warning
    annotations:
      summary: Container Volume usage (instance {{ $labels.instance }})
      description: "Container Volume usage is above 80%\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```
#### Container Volume IO usage
Container Volume IO usage is above 80%
```yaml
  - alert: ContainerVolumeIoUsage
    expr: (sum(container_fs_io_current) BY (instance, name) * 100) > 80
    for: 2m
    labels:
      severity: warning
    annotations:
      summary: Container Volume IO usage (instance {{ $labels.instance }})
      description: "Container Volume IO usage is above 80%\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```

#### Container high throttle rate
Container is being throttled
```yaml
# Если контейнер превышает лимит по CPU, то включается throttling - "урезание" квоты по CPU.Почитать про это, например:
# https://habr.com/ru/company/flant/blog/489668/
# https://www.itsumma.ru/knowledges/blog/CPUlimits
# и т.п.
  - alert: ContainerHighThrottleRate
    expr: rate(container_cpu_cfs_throttled_seconds_total[3m]) > 1
    for: 2m
    labels:
      severity: warning
    annotations:
      summary: "Container high throttle rate (instance {{ $labels.instance }})"
      description: "Container is being throttled\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
