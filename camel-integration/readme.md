# Camel Integration Dashboard

A health view of a Java integration service: how the application itself is doing (memory, garbage collection, threads) and how its integration routes are performing. It has two tabs — **JVM** and **Camel** — both filterable by **Service**.

## JVM

- **Memory Usage**: how much memory the application is using, broken down by memory area — the earliest signal of memory pressure before it becomes a real problem.
- **Garbage Collection**: how often and how long the application pauses to clean up memory; long or frequent pauses can cause visible slowdowns.
- **Threads**: how many threads are running and what they're doing (active, waiting, blocked) — a growing number of blocked threads often points to a bottleneck somewhere.
- **Class Loading**: general application activity, reflected in how many classes get loaded over time.
- **CPU Usage**: how much processing power the application and the machine it runs on are using.
- **Buffer Memory & Uptime**: additional memory usage and how long the process has been running without a restart.

## Camel

- **Active Routes**: how many integration routes are currently running.
- **Message Throughput**: how many messages are flowing through, and what share of them succeed or fail.
- **In-Flight Messages**: how many messages are being processed right now — a growing number can mean the integration is falling behind.
- **Route Processing Time**: how long each route takes to handle a message, on average and in the worst case.
- **Latency by Endpoint**: which type of destination (HTTP call, log, timer, ...) is the slowest.
- **Event Activity**: how often routes start, send, and complete messages — useful for spotting unusual patterns.

## How to Import

1. In OpenObserve, go to **Dashboards** and click **Import**.
2. Upload `camel-integration.dashboard.json`.
3. Make sure your application is sending its metrics to OpenObserve (e.g. via an OpenTelemetry agent and Micrometer).
4. Select the appropriate **Service** value to scope the dashboard to your instance.
