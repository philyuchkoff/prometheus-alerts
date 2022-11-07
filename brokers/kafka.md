# Kafka [Kafka Exporter](https://github.com/danielqsj/kafka_exporter)

## Kafka topics replicas   
##### Kafka topic in-sync partition
    
````
  - alert: KafkaTopicsReplicas
    expr: sum(kafka_topic_partition_in_sync_replica) by (topic) < 3
    for: 5m
    labels:
      severity: critical
    annotations:
      summary: "Kafka topics replicas (instance {{ $labels.instance }})"
      description: "Kafka topic in-sync partition\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
````
## Kafka consumers group  
##### Kafka consumers group
    
````
  - alert: KafkaConsumersGroup
    expr: sum(kafka_consumergroup_lag) by (consumergroup) > 50
    for: 5m
    labels:
      severity: critical
     annotations:
       summary: "Kafka consumers group (instance {{ $labels.instance }})"
       description: "Kafka consumers group\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
````
