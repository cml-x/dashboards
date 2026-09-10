# API Gateway Dashboard

Envoy sidecar monitoring dashboard for OpenObserve (`service_name=envoy`). It visualizes `cluster_*`, `http_*`, `listener_*`, `server_*`, `tls_*`, `dns_*`, `sds_*`, `overload_*`, `http2_*`, `filesystem_*`, `control_plane_*` and `access_logs_*` OpenTelemetry metrics. Panels are split into five tabs, all scoped by the **Service** and **Environment** variables.

> Note: `worker_pool_*` (Vert.x) and `netty_*` metrics look Envoy-related by name but actually belong to the application (`service_name=sap-sys`), not the Envoy sidecar — they are covered by the [Camel Integration](../Camel%20Integration) dashboard instead.

## Dashboard Features

### Traffic (`http_*`, `listener_*`)
- **Downstream Connections Active / Rate**: Active and new downstream connections, by listener.
- **HTTP Requests Rate**: Downstream requests per second, by listener.
- **Response Codes Rate**: Responses per second, by status class (2xx/4xx/5xx).
- **Request Duration (avg)**: Average request latency, by listener.
- **Downstream Connection Length (avg)**: Average connection duration, by listener.

### Upstream / Clusters (`cluster_*`)
- **Upstream Connections / Requests Active**: Live upstream activity, by cluster.
- **Upstream Requests Rate**: Throughput to each upstream cluster.
- **Upstream Response Codes Rate**: Responses per second, by cluster and status class.
- **Upstream Request Latency (avg) / Connect Time (avg)**: Cluster-level latency breakdown.
- **Circuit Breakers Open**: Connection/request/pending circuit breaker state, by cluster.
- **Upstream Pending Requests**: Requests queued for a connection.

### TLS / Security (`tls_*`, `listener_ssl_*`)
- **TLS Handshakes Rate**, **SSL Versions Rate**, **SSL Ciphers Rate**: TLS negotiation breakdown.
- **Certificate Expiration**: Days remaining before the first certificate expires.
- **TLS Inspector Bytes Processed / ALPN Detection**: TLS inspector filter activity.

### DNS / Control Plane (`dns_*`, `sds_*`, `control_plane_*`, `listener_manager_*`)
- **DNS Resolutions Rate / Timeouts / Pending**: c-ares DNS resolver health.
- **SDS Update Attempts Rate / Duration**: Secret discovery service activity.
- **Control Plane Connected State / Pending Requests**: xDS control plane connectivity.
- **LDS Update Success / Failure Rate**, **Active Listeners**: Listener discovery service health.

### Server / Resources (`server_*`, `overload_*`, `http2_*`, `filesystem_*`, `access_*`)
- **Server Live / Uptime**: Envoy process health.
- **Server Memory (Allocated / Heap)**, **Server Connections (Total / Parent)**.
- **Days Until First Cert Expiring**.
- **Overload Actions Active / Resource Pressure**: Overload manager state.
- **HTTP/2 Active Frames (Outbound)**: HTTP/2 multiplexing backlog.
- **Filesystem Buffered Writes**: Pending disk flushes.
- **Access Log Writes / Dropped Rate**: OpenTelemetry access log throughput.

## Variables

| Variable | Label | Source stream | Field |
| --- | --- | --- | --- |
| `service_name` | Service | `server_uptime` | `service_name` |
| `k8s_namespace_name` | Environment | `server_uptime` | `k8s_namespace_name` |

## Metrics Used

| Panel group | Metric streams |
| --- | --- |
| Traffic | `listener_downstream_cx_active`, `listener_downstream_cx_total`, `http_downstream_rq_total`, `listener_http_downstream_rq_xx`, `http_downstream_rq_time_sum/count`, `listener_downstream_cx_length_ms_sum/count` |
| Upstream / Clusters | `cluster_upstream_cx_active`, `cluster_upstream_rq_active/total/xx`, `cluster_upstream_rq_time_sum/count`, `cluster_upstream_cx_connect_ms_sum/count`, `cluster_circuit_breakers_cx_open/rq_open/rq_pending_open`, `cluster_upstream_rq_pending_active` |
| TLS / Security | `listener_ssl_handshake`, `listener_ssl_versions`, `listener_ssl_ciphers`, `listener_ssl_certificate_expiration_unix_time_seconds`, `tls_inspector_bytes_processed_sum`, `tls_inspector_alpn_found/not_found` |
| DNS / Control Plane | `dns_cares_resolve_total`, `dns_cares_timeouts`, `dns_cares_not_found`, `dns_cares_pending_resolutions`, `sds_update_attempt`, `sds_update_duration_sum/count`, `control_plane_connected_state`, `control_plane_pending_requests`, `listener_manager_lds_update_success/failure`, `listener_manager_total_listeners_active` |
| Server / Resources | `server_live`, `server_uptime`, `server_memory_allocated`, `server_memory_heap_size`, `server_total_connections`, `server_parent_connections`, `server_days_until_first_cert_expiring`, `overload_envoy_overload_actions_shrink_heap_active/stop_accepting_requests_active`, `overload_envoy_resource_monitors_fixed_heap_pressure/global_downstream_max_connections_pressure`, `http2_outbound_control_frames_active/frames_active`, `filesystem_write_total_buffered/write_buffered`, `access_logs_open_telemetry_access_log_logs_written/dropped` |

## How to Import

1. In OpenObserve, go to **Dashboards** and click **Import**.
2. Upload `API Gateway.dashboard.json`.
3. Make sure the Envoy metrics above are being ingested (Envoy admin stats sink via OpenTelemetry, `service_name=envoy`).
4. Select the appropriate **Service** and **Environment** values to scope the dashboard to your instance.
