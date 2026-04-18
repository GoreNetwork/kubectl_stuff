https://github.com/GoreNetwork/kubectl_stuff.git

Kubernetes Notes
See Cluster-arch.md
* Cluster arch
  * Master Nodes
    * kube-apiserver: controls the cluster
    * etcd cluster: key value pair
      * what container is on what ship, and info about the container
    * Kube Scheduler: what pods go on what nodes
    * Node Controller: handles adding/removing nodes
    * Replication Controller: makes sure correct pods are running at all times
  * Worker nodes
    * Container runtime engine
      * Everything is containers.  This runs the containers.
      * Docker or some equivalent
        * docker
        * containerd
        * rocket
    * kubelet: runs on every node in the cluster
      * Listens for instructions from api server
      * deploys/destroys pods as needed
      * API server fetches from kubelet to check status of nodes/containers
    * kube-proxy: makes sure the pods on worker nodes can reach other pods
  
