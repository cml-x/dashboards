# API Gateway Dashboard

A live view of your API gateway: how much traffic is flowing through it, how your backend services are responding, whether TLS certificates are healthy, and how the gateway itself is holding up. It's organized into five tabs, and everything can be filtered by **Service** and **Environment**.

> **Note:** a couple of panels that look like they'd belong here (JVM thread pools, low-level networking stats) actually describe the application behind the gateway, not the gateway itself — see the [Camel Integration](../camel-integration) dashboard for those.

## Traffic

| Panel | What it tells you |
| --- | --- |
| **Active Connections** | How many clients are connected right now, and how fast new ones are showing up. |
| **Requests per Second** | Overall traffic volume passing through the gateway. |
| **Response Codes** | The split between successful and failed responses — a spike in errors jumps out immediately. |
| **Request Duration** | How long requests take on average; a rising trend usually means something downstream is slowing down. |
| **Connection Length** | How long client connections typically stay open. |

## Backend Services

| Panel | What it tells you |
| --- | --- |
| **Active Connections & Requests** | How busy each backend service is at any given moment. |
| **Requests per Second** | How traffic is distributed across your backend services. |
| **Response Codes by Service** | Which backend is producing errors, if any. |
| **Latency & Connect Time** | How long each backend takes to respond and to establish a connection. |
| **Circuit Breakers** | Whether the gateway has started protecting itself by cutting off an overloaded backend. |
| **Pending Requests** | Requests waiting for a free connection to a backend — an early warning sign of saturation. |

## TLS & Security

| Panel | What it tells you |
| --- | --- |
| **Handshake Activity** | Volume of TLS negotiations, and which protocol/cipher versions clients are using. |
| **Certificate Expiration** | A countdown to when the TLS certificate needs renewing, so it never catches you by surprise. |
| **Encrypted Traffic Detection** | How the gateway identifies TLS traffic on its listeners. |

> **Tip:** keep an eye on Certificate Expiration — it's the single panel most likely to prevent an outage if you check it regularly.

## DNS & Control Plane

| Panel | What it tells you |
| --- | --- |
| **DNS Resolution Health** | Whether the gateway is successfully resolving backend hostnames, and how often lookups fail or time out. |
| **Configuration Sync** | Whether the gateway is receiving its TLS secrets and routing rules from the control plane without issues. |
| **Listener Health** | Whether the gateway's own network listeners are up and correctly configured. |

## Server & Resources

| Panel | What it tells you |
| --- | --- |
| **Health & Uptime** | Whether the gateway process is alive and how long it's been running. |
| **Memory & Connections** | The gateway's own resource footprint. |
| **Overload Protection** | Whether the gateway has triggered any self-protection mechanism under heavy load. |
| **Throughput Indicators** | Lower-level activity (multiplexed connections, buffered writes) useful for deeper troubleshooting. |
| **Access Log Throughput** | Whether access logs are being written and shipped without being dropped. |

## How to Import

1. In OpenObserve, go to **Dashboards** and click **Import**.
2. Upload `api-gateway.dashboard.json`.
3. Make sure your gateway is sending its metrics to OpenObserve via OpenTelemetry.
4. Select the appropriate **Service** and **Environment** values to scope the dashboard to your instance.
