## Kubernetes/Container Engine Visualizer

This is a simple visualizer for use with the Kubernetes API.

### Usage:
   * First install a Kubernetes or Container Engine Cluster
   * ```git clone https://github.com/brendandburns/gcp-live-k8s-visualizer.git```
   * ```kubectl proxy --www=path/to/gcp-live-k8s-visualizer --www-prefix=/my-mountpoint/ --api-prefix=/api/```

Then

    http://127.0.0.1:8001/my-mountpoint/

That's it.  The visualizer uses labels to organize the visualization.  In particular it expects that

   * pods, replicationcontrollers, and services have a ```name``` label, and pods and their associated replication controller share the same ```name```, and
   * the pods in your cluster will have a ```uses``` label which contains a comma separated list of services that the pod uses.
