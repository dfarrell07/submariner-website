+++
title = "Connectivity"
weight = 20
+++

### Connectivity Troubleshooting

Submariner deployment completed successfully but Services/Pods on one cluster are unable to connect to Services on another cluster. This can
be due to multiple factors outlined below.

#### Check the Connection Statistics

If you are unable to connect to a remote cluster, check its connection status in the Gateway resource.

`kubectl describe Gateway -n submariner-operator`

Sample output:

```yaml
   - endpoint:
        backend: libreswan
        cable_name: submariner-cable-cluster1-172-17-0-7
        cluster_id: cluster1
        healthCheckIP: 10.1.128.0
        hostname: cluster1-worker
        nat_enabled: false
        private_ip: 172.17.0.7
        public_ip: ""
        subnets:
        - 100.1.0.0/16
        - 10.1.0.0/16
      latencyRTT:
        average: 447.358µs
        last: 281.577µs
        max: 5.80437ms
        min: 158.725µs
        stdDev: 364.154µs
      status: connected
      statusMessage: Connected to 172.17.0.7:4500 - encryption alg=AES_GCM_16, keysize=128
        rekey-time=13444
```

{{% notice note %}}
This feature is only available for non-Globalnet deployments at the moment.
{{% /notice %}}

The Gateway Engine uses the `Health Check IP` of the endpoint to verify connectivity.
The connection `Status` will be marked as `error`, if it cannot reach this IP,
and the `Status Message` will provide more information about the possible failure reason.
It also provides the statistics for the connection.

<!---
#### IPSec tunnel not created between clusters

TBD

#### IPSEc tunnel is not up between clusters

TBD

#### None of pods/services able to connect to remote service

TBD

##### Without Globalnet

TBD

##### With Globalnet

TBD

#### Pods on non-gateway nodes not able to connect to remote service

TBD

##### Without Globalnet

TBD

##### With Globalnet

TBD

-->
