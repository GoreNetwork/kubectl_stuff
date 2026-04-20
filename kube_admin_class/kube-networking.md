* 1 kube pod can reach any other pod in the cluster via the pod network
  * An internal virtual network that spans across all nodes that all pods connect to 

* Service:
  * Expose the pods to other pods inside the cluster, or externally (NodePort, LoadBalancer)
    * Other pods uses the name of the service to access the pod the service is attached to
  * Service gets IP assigned
  * When kube-proxy sees a service it makes a rule using ip tables (or something like that)
    * Any traffic going to service IP goes to pod IP.