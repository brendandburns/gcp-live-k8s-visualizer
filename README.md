## Kubernetes/Container Engine Visualizer

This is a simple visualizer for use with the Kubernetes API.

### Usage:
   * First install a Kubernetes or Container Engine Cluster
   * ```git clone https://github.com/saturnism/gcp-live-k8s-visualizer.git```
   * ```kubectl proxy --www=path/to/gcp-live-k8s-visualizer```

That's it.  The visualizer uses labels to organize the visualization.  In particular it expects that

   * pods, replicationcontrollers, and services have a ```name``` label, and pods and their associated replication controller share the same ```name```, and
   * the pods in your cluster will have a ```uses``` label which contains a comma separated list of services that the pod uses.

### Installation on AWS:

   * First install a Kubernetes Cluster
   * On EC2 instance running the client (kubectl), install a proxy. We will be using HAProxy listening on port 80 for this guide.
   * ```sudo wget http://www.haproxy.org/download/1.6/src/haproxy-1.6.3.tar.gz```
   * ```sudo tar -xvf haproxy-1.6.3.tar.gz```
   * ```cd ./haproxy-1.6.3```
   * ```sudo make TARGET=linux2628 USE_PCRE=1 USE_OPENSSL=1 USE_ZLIB=1```
   * Create the following configuration file in /etc/haproxy.cfg:
     
     ```
    global
        daemon
        maxconn 256

    defaults
        mode http
        timeout connect 5000ms
        timeout client 50000ms
        timeout server 50000ms

    frontend http-in
        bind :80
        default_backend proxy-backend


    backend proxy-backend
        server proxy 127.0.0.1:8001
   ```

   * Startup the proxy:
    ```
    sudo ./haproxy -f /etc/haproxy.cfg
    ```
   * Startup kubernetes proxy by doing the following:
   * Get api server location, username, and password from kubernetes:
    ```
   kubectl config view
   ```
   * Create kubernetes proxy:
    ```
   kubectl proxy --www=path/to/k-visualizer/gcp-live-k8s-visualizer --username=admin --password=<password>  --accept-hosts="" --server="<server>" &
   ```
   * Access visualizer via Public IP of EC2 instance on which you created it:
    ```
   http://<public ip>/static/
   ```
