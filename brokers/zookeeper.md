## Zookeeper

###  [ZooKeeper Exporter](https://github.com/dabealu/zookeeper-exporter)

````
- name: Zookeeper
  rules:
  - alert: ZookeeperDown
    expr: zk_up == 0
    for: 0m
    labels:
      severity: critical
    annotations:
      summary: "Zookeeper Down (instance {{ $labels.instance }})"
      description: "Zookeeper down on instance {{ $labels.instance }}\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"

  - alert: ZookeeperMissingLeader
    expr: sum(zk_server_leader) == 0
    for: 0m
    labels:
      severity: critical
    annotations:
      summary: "Zookeeper missing leader (instance {{ $labels.instance }})"
      description: "Zookeeper cluster has no node marked as leader\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"

  - alert: ZookeeperTooManyLeaders
    expr: sum(zk_server_leader) > 1
    for: 0m
    labels:
      severity: critical
    annotations:
      summary: "Zookeeper Too Many Leaders (instance {{ $labels.instance }})"
      description: "Zookeeper cluster has too many nodes marked as leader\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"

  - alert: ZookeeperNotOk
    expr: zk_ruok == 0
    for: 3m
    labels:
      severity: warning
    annotations:
      summary: "Zookeeper Not Ok (instance {{ $labels.instance }})"
      description: "Zookeeper instance is not ok\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
````
