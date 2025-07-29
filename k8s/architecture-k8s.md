## K8S Architectures

Kubernetes follows client-server architecture where the Master Node and Worker node exist which constitutes a ‘Kubernetes Cluster’. 

We can have multiple worker nodes and Master nodes according to the requirement.


![Image](https://github.com/user-attachments/assets/9cb9b0dc-0722-4d3d-a72e-070ad309e9e1)


### Master Node :-

The master node is responsible for the entire Kubernetes cluster and manages all the activities inside the cluster.

Master nodes communicate with the worker node to run the applications on the containers smoothly. 


The components are `API server, etcd, controller manager & scheduler`



### Worker Node :-

The Worker Node is the mediator who manages and takes care of the containers and communicates with the Master Node which gives the instructions to assign the resources to the containers scheduled. 

A Kubernetes cluster can have multiple worker nodes to scale resources as needed.

The Worker Node contains four components : `kubelet , kube proxy , container engine and pod`



----------------------------------------
