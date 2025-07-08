## what is k8s ?

K8s (short for Kubernetes) is an open-source platform designed to automate the deployment, scaling, and management of containerized applications.

Kubernetes = Greek word for "helmsman" (someone who steers a ship 🚢).

K8s = shorthand where the 8 stands for the eight letters between "K" and "s."

It helps you orchestrate (coordinate) a bunch of containers across a cluster of machines, making sure everything runs smoothly — even if some machines fail.

Kubernetes (K8s) was officially launched by Google in 2014, now maintained by the Cloud Native Computing Foundation (CNCF).

Kubernetes is mainly written in Go (also known as Golang).

Think of it like :-

Instead of manually running Docker containers one by one.

Kubernetes automatically handles where and how they should run, updates them, restarts if they crash, and can even scale them up or down based on traffic.

## Why Kubernetes ?

When you have a few containers (like with Docker), it’s easy to manage them by hand.

But when you have hundreds or thousands (think big apps like Instagram, Netflix), you need :-

Automatic restarts if something crashes

Load balancing traffic

Scaling up and down based on user demand

Rolling out new updates without downtime

Moving apps between machines if one dies

Kubernetes automates all that, It's like the conductor of a huge orchestra — making sure every musician (container) plays in sync.

## K8S Architectures

Kubernetes follows client-server architecture where the Master Node and Worker node exist which constitutes a ‘Kubernetes Cluster’.

We can have multiple worker nodes and Master nodes according to the requirement.


`Master Node :-`

The master node is responsible for the entire Kubernetes cluster and manages all the activities inside the cluster.

Master nodes communicate with the worker node to run the applications on the containers smoothly.

EX- In a shopping mall, you have a management office that takes care of everything. In Kubernetes, this is the Master Node(management office).

The Master Node manages and coordinates all activities in the cluster, just like mall management ensures the mall runs smoothly.

The components are API server, etcd, controller manager & scheduler

### 1. API server :-

In Simple terms, after installing the kubectl(K8S CLI TOOL) on the master node developers run the commands to create pods. So, the command will go to the API Server, and then, the API Server forwards it to that component which will help to create the pods.

In other words, the API Server is an entry point for any Kubernetes task.

### 2. ETCD :-

Etcd is like a database that stores all the pieces of information of the Master node and Worker node(entire cluster) such as Pods IP, Nodes, networking configs, etc.

Etcd stored data in key-value pair. The data comes from the API Server also store in etcd.

### 3. Controller manager :-

The controller Manager collects the data/information from the API Server of the Kubernetes cluster like the desired state of the cluster and then decides what to do by sending the instructions to the API Server.

### 4. Scheduler :-

Once the API Server gathers the information from the Controller Manager, the API Server notifies the Scheduler to perform the respective task such as increasing the number of pods, etc. After getting notified, the Scheduler takes action on the provided work.

`Worker Node :-`

The Worker Node is the mediator who manages and takes care of the containers and communicates with the Master Node which gives the instructions to assign the resources to the containers scheduled.

A Kubernetes cluster can have multiple worker nodes to scale resources as needed.

The Worker Node contains four components : kubelet , kube proxy , container engine and pod

### 1. Kubelet :-

kubelet is the primary component of the Worker Node which manages the Pods and regularly checks whether the pod is running or not.

If pods are not working properly, then kubelet creates a new pod and replaces it with the previous one because the failed pod can’t be restarted hence, the IP of the pod might be changed.

Also , kubelet gets the details related to pods from the API Server which exists on the Master Node.

### 2. Kube-proxy :-

kube-proxy contains all the network configuration of the entire cluster such as pod IP, etc.

Kube-proxy takes care of the load balancing and routing which comes under networking configuration.

Kube-proxy gets the information about pods from the API Server which exists on Master Node.

### 3. Container engine :-

To provide the runtime environment to the container, Container Engine is used.

In Kubernetes, the Container engine directly interacts with container runtime which is responsible for creating and managing the containers.

There are a lot of Container engines present in the market such as CRI-O, containerd, rkt(rocket), etc. But Docker is one of the most used and trusted Container Engine.

### 4. Pod :-

Pod is a very small unit that contains a container or multiple containers where the application is deployed.

Pod has a Public or Private IP range that distributes the proper IP to the containers.

It’s good to have one container under each pod.
