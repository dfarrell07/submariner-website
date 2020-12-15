+++
title = "Prometheus Metrics"
date = 2020-08-12T16:02:00+02:00
weight = 20
+++

## Basic Overview

Submariner provides a number of [Prometheus](https://prometheus.io/) metrics, and sets up `ServiceMonitor` instances which allow these
metrics to be scraped by an in-cluster Prometheus deployment. Prometheus is a pluggable metrics collection and storage system and can act as
a data source for [Grafana](https://grafana.com/), a metrics visualization frontend. Unlike some metrics collectors, Prometheus requires the
collectors to pull metrics from each source.

## Exposed Metrics

Submariner metrics provide insights into both the state of Submariner itself, as well as the inter-cluster network behavior of your
cluster set. All Submariner metrics are exported within the `submariner-operator` namespace by default.

The following metrics are exposed currently:

* `submariner_gateways`: the number of gateways in the cluster

* `submariner_connections`: the number of connections to other clusters, with the following labels:

  * `local_cluster`: the local cluster name
  * `local_hostname`: the local hostname
  * `remote_cluster`: the remote cluster name
  * `remote_hostname`: the remote hostname
  * `status`: the connection status (“connecting”, “connected”, or “error”)

* `gateway_rx_bytes`: count of bytes received by cable driver and cable (labels: `cable_driver`, `local_cluster`, `local_hostname`,
`local_endpoint_ip`, `remote_cluster`, `remote_hostname`, `remote_endpoint_ip`)

* `gateway_tx_bytes`: count of bytes transmitted by cable driver and cable (labels: `cable_driver`, `local_cluster`, `local_hostname`,
`local_endpoint_ip`, `remote_cluster`, `remote_hostname`, `remote_endpoint_ip`)

* `connection_established_timestamp`: timestamp of last successful connection established by cable driver and cable
(labels: `cable_driver`, `local_cluster`, `local_hostname`, `local_endpoint_ip`, `remote_cluster`, `remote_hostname`, `remote_endpoint_ip`)

* `connection_latency_seconds`: connection latency in seconds; last RTT, by cable driver and cable
(labels: `cable_driver`, `local_cluster`, `local_hostname`, `local_endpoint_ip`, `remote_cluster`, `remote_hostname`, `remote_endpoint_ip`)

* `connections`: the number of connections and corresponding status by cable driver and cable
(labels: `cable_driver`, `local_cluster`, `local_hostname`, `local_endpoint_ip`, `remote_cluster`, `remote_hostname`, `remote_endpoint_ip`,
`status`)
