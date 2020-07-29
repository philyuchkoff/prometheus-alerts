## Elasticsearch

###  [Elasticsearch Exporter](https://github.com/justwatchcom/elasticsearch_exporter)


-   #### Elasticsearch Heap Usage Too High
    
##### The heap usage is over 90% for 5m
    
```yaml
      - alert: ElasticsearchHeapUsageTooHigh
        expr: (elasticsearch_jvm_memory_used_bytes{area="heap"} / elasticsearch_jvm_memory_max_bytes{area="heap"}) * 100 > 90
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Elasticsearch Heap Usage Too High (instance {{ $labels.instance }})"
          description: "The heap usage is over 90% for 5m\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Elasticsearch Heap Usage warning
    
##### The heap usage is over 80% for 5m
    
```yaml
      - alert: ElasticsearchHeapUsageWarning
        expr: (elasticsearch_jvm_memory_used_bytes{area="heap"} / elasticsearch_jvm_memory_max_bytes{area="heap"}) * 100 > 80
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Elasticsearch Heap Usage warning (instance {{ $labels.instance }})"
          description: "The heap usage is over 80% for 5m\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Elasticsearch disk space low
    
##### The disk usage is over 80%
    
```yaml
      - alert: ElasticsearchDiskSpaceLow
        expr: elasticsearch_filesystem_data_available_bytes / elasticsearch_filesystem_data_size_bytes * 100 < 20
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Elasticsearch disk space low (instance {{ $labels.instance }})"
          description: "The disk usage is over 80%\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Elasticsearch disk out of space
    
##### The disk usage is over 90%
    
```yaml
      - alert: ElasticsearchDiskOutOfSpace
        expr: elasticsearch_filesystem_data_available_bytes / elasticsearch_filesystem_data_size_bytes * 100 < 10
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Elasticsearch disk out of space (instance {{ $labels.instance }})"
          description: "The disk usage is over 90%\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Elasticsearch Cluster Red
    
##### Elastic Cluster Red status
    
```yaml
      - alert: ElasticsearchClusterRed
        expr: elasticsearch_cluster_health_status{color="red"} == 1
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Elasticsearch Cluster Red (instance {{ $labels.instance }})"
          description: "Elastic Cluster Red status\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Elasticsearch Cluster Yellow
    
##### Elastic Cluster Yellow status
    
```yaml
      - alert: ElasticsearchClusterYellow
        expr: elasticsearch_cluster_health_status{color="yellow"} == 1
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Elasticsearch Cluster Yellow (instance {{ $labels.instance }})"
          description: "Elastic Cluster Yellow status\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Elasticsearch Healthy Nodes
    
##### Number Healthy Nodes less then number_of_nodes
    
```yaml
      - alert: ElasticsearchHealthyNodes
        expr: elasticsearch_cluster_health_number_of_nodes < number_of_nodes
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Elasticsearch Healthy Nodes (instance {{ $labels.instance }})"
          description: "Number Healthy Nodes less then number_of_nodes\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Elasticsearch Healthy Data Nodes
    
##### Number Healthy Data Nodes less then number_of_data_nodes
    
```yaml
      - alert: ElasticsearchHealthyDataNodes
        expr: elasticsearch_cluster_health_number_of_data_nodes < number_of_data_nodes
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Elasticsearch Healthy Data Nodes (instance {{ $labels.instance }})"
          description: "Number Healthy Data Nodes less then number_of_data_nodes\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Elasticsearch relocation shards
    
##### Number of relocation shards for 20 min
    
```yaml
      - alert: ElasticsearchRelocationShards
        expr: elasticsearch_cluster_health_relocating_shards > 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Elasticsearch relocation shards (instance {{ $labels.instance }})"
          description: "Number of relocation shards for 20 min\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Elasticsearch initializing shards
    
##### Number of initializing shards for 10 min
    
```yaml
      - alert: ElasticsearchInitializingShards
        expr: elasticsearch_cluster_health_initializing_shards > 0
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Elasticsearch initializing shards (instance {{ $labels.instance }})"
          description: "Number of initializing shards for 10 min\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Elasticsearch unassigned shards
    
##### Number of unassigned shards for 2 min
    
```yaml
      - alert: ElasticsearchUnassignedShards
        expr: elasticsearch_cluster_health_unassigned_shards > 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Elasticsearch unassigned shards (instance {{ $labels.instance }})"
          description: "Number of unassigned shards for 2 min\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Elasticsearch pending tasks
    
##### Number of pending tasks for 10 min. Cluster works slowly
    
```yaml
      - alert: ElasticsearchPendingTasks
        expr: elasticsearch_cluster_health_number_of_pending_tasks > 0
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Elasticsearch pending tasks (instance {{ $labels.instance }})"
          description: "Number of pending tasks for 10 min. Cluster works slowly.\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
    
      
    
-   #### Elasticsearch no new documents
    
##### No new documents for 10 min!
    
```yaml
      - alert: ElasticsearchNoNewDocuments
        expr: rate(elasticsearch_indices_docs{es_data_node="true"}[10m]) < 1
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Elasticsearch no new documents (instance {{ $labels.instance }})"
          description: "No new documents for 10 min!\n  VALUE = {{ $value }}\n  LABELS: {{ $labels }}"
```
