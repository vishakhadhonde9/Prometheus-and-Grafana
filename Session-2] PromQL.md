# PromQL -
- PromQL stands for Prometheus Query Language.
- It is used to query time-series data stored in Prometheus.

# Components of PromoQL -

## Metrics -
- A metric is something you measure.
- Examples-
  - Number of HTTP requests (http_requests_total)
  - CPU usage (node_cpu_seconds_total)
  - Memory free (node_memory_free_bytes)
  - Disk usage (node_disk_io_time_seconds_total)
 
## Label -
- A label is extra information about a metric.
- Labels help you filter or group your data.
  - method: GET
  - status code: 200
  - application: frontend


## Selectors -
- {} inside a metric helps select specific series.
- Empty {} means "select all time series for this metric".

    node_cpu_seconds_total{method="GET"}

## Functions -
- Functions transform the data.
- Common ones are:
  - rate(metric[5m]) → Average per-second rate over last 5 minutes (good for counters).
  - irate(metric[5m]) → Instantaneous rate (last 2 points, faster response).
  - avg() → Average.
  - sum() → Sum.

## Operators -

| Operator | Meaning | Example |
|:---------|:--------|:--------|
| `+` | Add | `http_requests_total + errors_total` |
| `-` | Subtract | `total_memory - free_memory` |
| `*` | Multiply | `cpu_idle * 100` (to get percent) |
| `/` | Divide | `used_memory / total_memory` |
| `>` | Greater than | `cpu_usage > 80` |
| `<` | Less than | `disk_free < 10` |
| `==` | Equal to | `status == 1` |
| `!=` | Not equal to | `job != "backup"` |



      Start
       ↓
      Choose a Metric (example: http_requests_total)
       ↓
      Optionally Filter it (example: {method="GET"})
       ↓
      Optionally Apply Function (example: rate() or sum())
       ↓
      Result!

# rule.yml -

    groups:
    - name: example-group
      rules:
      - alert: HighCPUUsage
        expr: 100 - (avg by (instance) (irate(node_cpu_seconds_total{mode="idle"}[5m])) * 100) > 1
        for: 1m
        labels:
          severity: critical
        annotations:
          summary: "High CPU Usage detected (instance {{ $labels.instance }})"
          description: "CPU usage is above 1% for 1 minutes on instance {{ $labels.instance }}"


## Change configuration File for Rules -


    # Alertmanager configuration
    alerting:
      alertmanagers:
        - static_configs:
            - targets:
               - alertmanager:9093
    
    # Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
    rule_files:
        - "rules.yml"
      # - "second_rules.yml"


- sudo systemctl restart prometheus node_exporter
