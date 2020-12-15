+++
title = "Monitoring"
date = 2020-08-12T16:02:00+02:00
weight = 20
+++

## Basic Overview

Submariner provides a number of [Prometheus](https://prometheus.io/) metrics, and sets up `ServiceMonitor` instances which allow these
metrics to be scraped by an in-cluster Prometheus deployment. Prometheus is a pluggable metrics collection and storage system and can act as
a data source for [Grafana](https://grafana.com/), a metrics visualization frontend. Unlike some metrics collectors, Prometheus requires the
collectors to pull metrics from each source.

### Prometheus Operator

To start monitoring Submariner using the Prometheus Operator, Prometheus needs to be configured to scrape the Submariner Operator’s
namespace (`submariner-operator` by default). The specifics depend on your Prometheus deployment, but typically, this will require
you to:

* Add the Submariner Operator’s namespace to Prometheus’ `ClusterRoleBinding`.

* Ensure that Prometheus’ configuration doesn’t prevent it from scraping this namespace.

A minimal `Prometheus` object providing access to the Submariner metrics is as follows:

```yaml
apiVersion: monitoring.coreos.com/v1
kind: Prometheus
metadata:
  name: prometheus
  labels:
    prometheus: prometheus
spec:
  replicas: 1
  serviceAccountName: prometheus
  serviceMonitorNamespaceSelector: {}
  serviceMonitorSelector:
    matchLabels:
      name: submariner-operator
```

### OpenShift Setup

OpenShift 4.5 or later can automatically discover the Submariner metrics.
This requires enabling user workload monitoring; see the
[OpenShift 4.5](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.5/html/monitoring/monitoring-your-own-services)
or
[OpenShift 4.6](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.6/html/monitoring/enabling-monitoring-for-user-defined-projects)
documentation for details.
