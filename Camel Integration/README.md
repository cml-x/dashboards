# Camel Integration Dashboard

JVM and Apache Camel monitoring dashboard for OpenObserve. It visualizes `jvm_*` / `process_*` / `system_*` and `camel_*` OpenTelemetry metrics for an Apache Camel integration service. Panels are split into two tabs: **JVM** and **Camel**, both scoped by the **Service** variable (`service_name`).

## Dashboard Features

### JVM tab

- **JVM Memory Used (Heap / Non-Heap)**: Memory usage per pool (`Eden Space`, `Survivor Space`, `Tenured Gen`, `Metaspace`, `Compressed Class Space`, code heaps).
- **JVM GC Pause Duration / Rate**: Average garbage collection pause time and pause frequency, by collector.
- **JVM Threads**: Live, daemon and peak thread counts.
- **JVM Thread States**: Thread count by state (`runnable`, `blocked`, `waiting`, `timed-waiting`, `new`, `terminated`).
- **JVM Classes Loaded / Unloaded**: Class loading activity.
- **CPU Usage**: Process vs. system CPU usage (%).
- **JVM Buffer Memory Used**: Direct/mapped buffer memory.
- **Process Uptime**: JVM process uptime.

### Camel tab

- **Camel Routes Running**: Number of active routes per Camel context.
- **Exchanges Rate / Succeeded Rate / Failure Rate**: Exchange throughput and success/failure rate, by route.
- **Exchanges Inflight**: Exchanges currently being processed, by route.
- **Route Processing Time (avg / max)**: Route latency, by route.
- **Exchange Latency by Endpoint (avg)**: Average exchange duration, by endpoint (`platform-http`, `log`, `timer`, ...).
- **Exchange Events by Type**: Notifier event rate, by event type (`ExchangeCompletedEvent`, `ExchangeSentEvent`).

## Variable

| Variable | Label | Source stream | Field |
| --- | --- | --- | --- |
| `service_name` | Service | `process_uptime` | `service_name` |

## Metrics Used

| Panel | Metric stream(s) |
| --- | --- |
| JVM Memory Used | `jvm_memory_used` |
| GC Pause | `jvm_gc_pause_sum`, `jvm_gc_pause_count` |
| Threads | `jvm_threads_live`, `jvm_threads_daemon`, `jvm_threads_peak` |
| Thread States | `jvm_threads_states` |
| Classes | `jvm_classes_loaded`, `jvm_classes_unloaded` |
| CPU Usage | `process_cpu_usage`, `system_cpu_usage` |
| Buffer Memory | `jvm_buffer_memory_used` |
| Uptime | `process_uptime` |
| Routes Running | `camel_routes_running` |
| Exchanges | `camel_exchanges_total`, `camel_exchanges_succeeded`, `camel_exchanges_inflight` |
| Route Processing Time | `camel_route_policy_sum`, `camel_route_policy_count`, `camel_route_policy_max` |
| Exchange Latency by Endpoint | `camel_exchange_event_notifier_sum`, `camel_exchange_event_notifier_count` |
| Exchange Events by Type | `camel_exchange_event_notifier_count` |

## How to Import

1. In OpenObserve, go to **Dashboards** and click **Import**.
2. Upload `Camel Integration.dashboard.json`.
3. Make sure the JVM/Camel metrics above are being ingested (e.g. via an OpenTelemetry Java agent + Micrometer on your Camel application).
4. Select the appropriate **Service** value to scope the dashboard to your instance.
