## RabbitMQ

### [RabbitMQ Exporter](https://github.com/rabbitmq/rabbitmq-prometheus)

-   #### Rabbitmq down
    
##### RabbitMQ node down
    
```yaml
      - alert: RabbitmqDown
        expr: rabbitmq_up == 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Rabbitmq down (instance {{ $labels.instance }})"
          description: "RabbitMQ node down\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
-   #### Rabbitmq cluster down
    
##### Less than 3 nodes running in RabbitMQ cluster
    
```yaml
      - alert: RabbitmqClusterDown
        expr: sum(rabbitmq_running) < 3
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Rabbitmq cluster down (instance {{ $labels.instance }})"
          description: "Less than 3 nodes running in RabbitMQ cluster\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Rabbitmq cluster partition
    
##### Cluster partition
    
```yaml
      - alert: RabbitmqClusterPartition
        expr: rabbitmq_partitions > 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Rabbitmq cluster partition (instance {{ $labels.instance }})"
          description: "Cluster partition\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Rabbitmq out of memory
    
##### Memory available for RabbmitMQ is low (< 10%)
    
```yaml
      - alert: RabbitmqOutOfMemory
        expr: rabbitmq_node_mem_used / rabbitmq_node_mem_limit * 100 > 90
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Rabbitmq out of memory (instance {{ $labels.instance }})"
          description: "Memory available for RabbmitMQ is low (< 10%)\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
-   #### RabbitMQ memory high
    
##### A node use more than 90% of allocated RAM      
```yaml
  - alert: RabbitmqMemoryHigh
    expr: rabbitmq_process_resident_memory_bytes / rabbitmq_resident_memory_limit_bytes * 100 > 90
    for: 2m
    labels:
      severity: warning
    annotations:
      summary: Rabbitmq memory high (instance {{ $labels.instance }})
      description: "A node use more than 90% of allocated RAM\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```

-   #### Rabbitmq file descriptors usage
    
##### A node use more than 90% of file descriptors      
```yaml
  - alert: RabbitmqFileDescriptorsUsage
    expr: rabbitmq_process_open_fds / rabbitmq_process_max_fds * 100 > 90
    for: 2m
    labels:
      severity: warning
    annotations:
      summary: Rabbitmq file descriptors usage (instance {{ $labels.instance }})
      description: "A node use more than 90% of file descriptors\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```

-   #### RabbitMQ too many unack messages
    
##### Too many unacknowledged messages      
```yaml
  - alert: RabbitmqTooManyUnackMessages
    expr: sum(rabbitmq_queue_messages_unacked) BY (queue) > 1000
    for: 1m
    labels:
      severity: warning
    annotations:
      summary: Rabbitmq too many unack messages (instance {{ $labels.instance }})
      description: "Too many unacknowledged messages\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```

-   #### Rabbitmq too many connections
    
##### RabbitMQ instance has too many connections (> 1000)
    
```yaml
      - alert: RabbitmqTooManyConnections
        expr: rabbitmq_connectionsTotal > 1000
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Rabbitmq too many connections (instance {{ $labels.instance }})"
          description: "RabbitMQ instance has too many connections (> 1000)\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
 -   #### RabbitMQ no queue consumer
    
##### A queue has less than 1 consumer
    
```yaml
  - alert: RabbitmqNoQueueConsumer
    expr: rabbitmq_queue_consumers < 1
    for: 1m
    labels:
      severity: warning
    annotations:
      summary: Rabbitmq no queue consumer (instance {{ $labels.instance }})
      description: "A queue has less than 1 consumer\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```   
      
    
-   #### Rabbitmq dead letter queue filling up
    
##### Dead letter queue is filling up (> 10 msgs)
    
```yaml
      - alert: RabbitmqDeadLetterQueueFillingUp
        expr: rabbitmq_queue_messages{queue="my-dead-letter-queue"} > 10
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Rabbitmq dead letter queue filling up (instance {{ $labels.instance }})"
          description: "Dead letter queue is filling up (> 10 msgs)\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Rabbitmq too many messages in queue
    
##### Queue is filling up (> 1000 msgs)
    
```yaml
      - alert: RabbitmqTooManyMessagesInQueue
        expr: rabbitmq_queue_messages_ready{queue="my-queue"} > 1000
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Rabbitmq too many messages in queue (instance {{ $labels.instance }})"
          description: "Queue is filling up (> 1000 msgs)\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Rabbitmq slow queue consuming
    
##### Queue messages are consumed slowly (> 60s)
    
```yaml
      - alert: RabbitmqSlowQueueConsuming
        expr: time() - rabbitmq_queue_head_message_timestamp{queue="my-queue"} > 60
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Rabbitmq slow queue consuming (instance {{ $labels.instance }})"
          description: "Queue messages are consumed slowly (> 60s)\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Rabbitmq no consumer
    
##### Queue has no consumer
    
```yaml
      - alert: RabbitmqNoConsumer
        expr: rabbitmq_queue_consumers == 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Rabbitmq no consumer (instance {{ $labels.instance }})"
          description: "Queue has no consumer\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Rabbitmq too many consumers
    
##### Queue should have only 1 consumer
    
```yaml
      - alert: RabbitmqTooManyConsumers
        expr: rabbitmq_queue_consumers > 1
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Rabbitmq too many consumers (instance {{ $labels.instance }})"
          description: "Queue should have only 1 consumer\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Rabbitmq unactive exchange
    
##### Exchange receive less than 5 msgs per second[copy]
    
```yaml
      - alert: RabbitmqUnactiveExchange
        expr: rate(rabbitmq_exchange_messages_published_in_total{exchange="my-exchange"}[1m]) < 5
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Rabbitmq unactive exchange (instance {{ $labels.instance }})"
          description: "Exchange receive less than 5 msgs per second\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
