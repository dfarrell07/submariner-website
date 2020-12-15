+++
title = "Troubleshooting"
weight = 10
+++

## Overview

You have followed steps in [Deployment](../deployment) but something has gone wrong. You're not sure what and how to fix it, or what
information to collect to raise an issue. Welcome to the Submariner troubleshooting guide where we will help you get your deployment working
again.

Basic familiarity with the Submariner components and architecture will be helpful when troubleshooting so please review the
[Architecture](../../getting-started/architecture) section.

The guide has been broken into different sections for easy navigation.

### Pre-requisite

Before we begin troubleshooting, run `subctl version` to obtain which version of the Submariner components you are running.

Run `kubectl get services -n <service-namespace> | grep <service-name>` to get information about the service you're trying to access. This
will provide you with the Service *Name*, *Namespace* and *ServiceIP*. If **Globalnet** is enabled, you will also need the *globalIp* of the
service by running

`kubectl get service <service-name> -o jsonpath='{.metadata.annotations.submariner\.io/globalIp}'`


