# Dashboards

Public dashboards maintained by Camel X, for monitoring with [OpenObserve](https://openobserve.ai/). Each dashboard is a JSON file that can be imported directly into OpenObserve.

This repo currently covers our own services, but is meant to grow into a general collection covering all kinds of monitoring targets over time.

## Available dashboards

| Dashboard | Description |
| --- | --- |
| [api-gateway](api-gateway) | Envoy sidecar monitoring (traffic, upstream clusters, TLS, DNS/control plane, server resources) |
| [camel-integration](camel-integration) | JVM and Apache Camel monitoring (memory, GC, threads, routes, exchanges) |

## How to use

1. Download the `.dashboard.json` file for the dashboard you want.
2. In OpenObserve, go to **Dashboards** and click **Import**.
3. Select the downloaded file.
4. Click **Import**.

## How to contribute

1. Fork this repository.
2. Create a new branch.
3. Add your dashboard in a new lowercase, hyphenated folder (e.g. `my-dashboard/`), including a `.dashboard.json` file and a `readme.md` describing it. A screenshot is appreciated but not required.
4. Open a pull request.

## License

Apache 2.0 — see [LICENSE](LICENSE).
