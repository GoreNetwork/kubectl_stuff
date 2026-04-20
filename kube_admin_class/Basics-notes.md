https://github.com/GoreNetwork/kubectl_stuff.git

Kubernetes Notes
See Cluster-arch.md
* Cluster arch
  * Master Nodes
    * kube-apiserver: controls the cluster
    * etcd cluster: distributed key-value store
      * stores all cluster state: node info, pod specs, ConfigMaps, Secrets, service accounts, etc.
    * Kube Scheduler: what pods go on what nodes
    * Node Controller: handles adding/removing nodes
    * Replication Controller: makes sure correct pods are running at all times
  * Worker nodes
    * Container runtime engine
      * Everything is containers.  This runs the containers.
      * containerd (which Docker is built on) or some equivalent
        * containerd
        * CRI-O
    * kubelet: runs on every node in the cluster
      * Listens for instructions from api server
      * deploys/destroys pods as needed
      * API server fetches from kubelet to check status of nodes/containers
    * kube-proxy: makes sure the pods on worker nodes can reach other pods
  
* etcd
  * Distributed key value store
    * basically a dict
      * Something like user: {age: 25, location: nyc, salary=50000}
      * Or something simpler like just {salary: 5000}
* kubeapi server
  * pulls data from etcd server and responds back to api user
  * does things like
    * Auth
    * validate request
    * retrieve data
    * update etcd
    * scheduler uses it to perform tasks like deploying a pod to a worker node's kubelet
* Controller
  * Continuously monitors state of components and brings system to desired state
    * Examples
      * Node Controller monitors nodes and keeps apps running (Via API server)
      * Replica Set Controller: makes sure enough pods are up and kicking
      * Lots of these

* Kube Scheduler
  * Decides which pod goes on which node
    * Doesn't actually place the pod, but decides which node the pod goes on
  *  How does it decide?
     *  Filter Nodes: based on requirements: pod takes 10mb node as 1mb, that pod gets filtered out.
     *  Rank Node: 0-10.  How much resources are left over after the pod is added
     *  Taints, tolerations, node selectors, affinity, etc

* Kubelet:
  * gets everything done on worker node 
    * adds node to cluster
    * makes/remove pods
  * reports back everything

* kube proxy
  * Runs on each node in cluster
  * Looks for new service
    * When new service is found it creates rules to forward traffic to the pod the service references.
      * IP tables rules: traffic going to service IP  is forwarded to pod IP