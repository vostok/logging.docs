# Initial page

Vostok provides instrumentation for microservices and a number of Vostok infrastructure components. Instrumentation is required to collect data which is necessary for any production-ready distributed system:

* logs for application lifecycle
* metrics for resource usage
* traces for intra-cluster interaction

Every Vostok-instrumented microservice collects described data out of the box. No additional confuguration or code is required.

Applications would use provided interfaces to write custom logs and metrics. Any outgoing requests via provided [Cluster Client](https://github.com/vostok/core/tree/master/Vostok.ClusterClient) would be included to collected distributed traces. These include requests to Vostok-instrumented applications \(e.g., other microservices\) and non-instrumented applications \(e.g., databases or external APIs\).

