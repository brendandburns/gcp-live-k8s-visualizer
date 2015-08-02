## Kubernetes/Container Engine Visualizer

This is a simple visualizer for use with the Kubernetes API.

### Usage:
   * First install a Kubernetes or Container Engine Cluster
   * ```git clone https://github.com/brendandburns/gcp-live-k8s-visualizer.git```
   * ```kubecfg proxy --www=path/to/gcp-live-k8s-visualizer```

That's it.  The visualizer uses labels to organize the visualization.  In particular it expects that the pods in your cluster will have a ```uses``` label which contains a comma separated list of services that the pod uses.
