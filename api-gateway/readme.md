# API Gateway Dashboard

A live view of your API gateway: how much traffic is flowing through it, how your backend services are responding, whether TLS certificates are healthy, and how the gateway itself is holding up. It's organized into five tabs, and everything can be filtered by **Service** and **Environment**.

> Note: a couple of panels that look like they'd belong here (JVM thread pools, low-level networking stats) actually describe the application behind the gateway, not the gateway itself — see the [Camel Integration](../camel-integration) dashboard for those.

## Traffic

- **Active Connections**: how many clients are connected right now, and how fast new ones are showing up.
- **Requests per Second**: overall traffic volume passing through the gateway.
- **Response Codes**: the split between successful and failed responses — a spike in errors jumps out immediately.
- **Request Duration**: how long requests take on average; a rising trend usually means something downstream is slowing down.
- **Connection Length**: how long client connections typically stay open.

## Backend Services

- **Active Connections & Requests**: how busy each backend service is at any given moment.
- **Requests per Second**: how traffic is distributed across your backend services.
- **Response Codes by Service**: which backend is producing errors, if any.
- **Latency & Connect Time**: how long each backend takes to respond and to establish a connection.
- **Circuit Breakers**: whether the gateway has started protecting itself by cutting off an overloaded backend.
- **Pending Requests**: requests waiting for a free connection to a backend — an early warning sign of saturation.

## TLS & Security

- **Handshake Activity**: volume of TLS negotiations, and which protocol/cipher versions clients are using.
- **Certificate Expiration**: a countdown to when the TLS certificate needs renewing, so it never catches you by surprise.
- **Encrypted Traffic Detection**: how the gateway identifies TLS traffic on its listeners.

## DNS & Control Plane

- **DNS Resolution Health**: whether the gateway is successfully resolving backend hostnames, and how often lookups fail or time out.
- **Configuration Sync**: whether the gateway is receiving its TLS secrets and routing rules from the control plane without issues.
- **Listener Health**: whether the gateway's own network listeners are up and correctly configured.

## Server & Resources

- **Health & Uptime**: whether the gateway process is alive and how long it's been running.
- **Memory & Connections**: the gateway's own resource footprint.
- **Overload Protection**: whether the gateway has triggered any self-protection mechanism under heavy load.
- **Throughput Indicators**: lower-level activity (multiplexed connections, buffered writes) useful for deeper troubleshooting.
- **Access Log Throughput**: whether access logs are being written and shipped without being dropped.

## How to Import

1. In OpenObserve, go to **Dashboards** and click **Import**.
2. Upload `api-gateway.dashboard.json`.
3. Make sure your gateway is sending its metrics to OpenObserve via OpenTelemetry.
4. Select the appropriate **Service** and **Environment** values to scope the dashboard to your instance.
