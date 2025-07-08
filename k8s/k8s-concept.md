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

#### 1. API server :-

In Simple terms, after installing the kubectl(K8S CLI TOOL) on the master node developers run the commands to create pods. So, the command will go to the API Server, and then, the API Server forwards it to that component which will help to create the pods.

In other words, the API Server is an entry point for any Kubernetes task.

#### 2. ETCD :-

Etcd is like a database that stores all the pieces of information of the Master node and Worker node(entire cluster) such as Pods IP, Nodes, networking configs, etc.

Etcd stored data in key-value pair. The data comes from the API Server also store in etcd.

#### 3. Controller manager :-

The controller Manager collects the data/information from the API Server of the Kubernetes cluster like the desired state of the cluster and then decides what to do by sending the instructions to the API Server.

#### 4. Scheduler :-

Once the API Server gathers the information from the Controller Manager, the API Server notifies the Scheduler to perform the respective task such as increasing the number of pods, etc. After getting notified, the Scheduler takes action on the provided work.

`Worker Node :-`

The Worker Node is the mediator who manages and takes care of the containers and communicates with the Master Node which gives the instructions to assign the resources to the containers scheduled.

A Kubernetes cluster can have multiple worker nodes to scale resources as needed.

The Worker Node contains four components : kubelet , kube proxy , container engine and pod

#### 1. Kubelet :-

kubelet is the primary component of the Worker Node which manages the Pods and regularly checks whether the pod is running or not.

If pods are not working properly, then kubelet creates a new pod and replaces it with the previous one because the failed pod can’t be restarted hence, the IP of the pod might be changed.

Also , kubelet gets the details related to pods from the API Server which exists on the Master Node.

#### 2. Kube-proxy :-

kube-proxy contains all the network configuration of the entire cluster such as pod IP, etc.

Kube-proxy takes care of the load balancing and routing which comes under networking configuration.

Kube-proxy gets the information about pods from the API Server which exists on Master Node.

#### 3. Container engine :-

To provide the runtime environment to the container, Container Engine is used.

In Kubernetes, the Container engine directly interacts with container runtime which is responsible for creating and managing the containers.

There are a lot of Container engines present in the market such as CRI-O, containerd, rkt(rocket), etc. But Docker is one of the most used and trusted Container Engine.

#### 4. Pod :-

Pod is a very small unit that contains a container or multiple containers where the application is deployed.

Pod has a Public or Private IP range that distributes the proper IP to the containers.

It’s good to have one container under each pod.


## ## what is pod ?


Kubernetes doesn't manage containers directly—it manages pods. 

A Kubernetes (k8s) pod is the smallest and simplest unit in the Kubernetes object model that you can create or deploy and manage.

A pod is a wrapper around one or more containers (usually Docker containers) that are deployed together on the same host, share the same network and storage, and are treated as a single unit.

A pod can run a single container or multiple tightly coupled containers that share the same resources.

Pods are ephemeral. If a pod dies, Kubernetes can automatically create a new pod, but it will be a new instance with a different IP.

All containers in a pod share the same IP and port space.

Containers in a pod are started, stopped, and managed together.


### How to create pod inside default namespace ?


##### step-1 :- create yaml file for pod create


```bash
vi mypodcrt.yml
```


##### step-2 :- use below command for pod create


`A. If it is kubeadm then👇👇`


```
apiVersion: v1
kind: Pod
metadata:
  name: pod1
spec:
  nodeSelector:
    kubernetes.io/hostname: worker-1
  containers:
    - name: container1
      image: nginx
      ports:
        - containerPort: 80

```


`B. If it is minikube then👇👇`


```
apiVersion: v1
kind: Pod
metadata:
  name: pod1
spec:
  containers:
  - name: container1
    image: nginx
    ports:
    - containerPort: 80

```


##### step-3 :- apply the manifest file(mypodcrt.yml) to create the pod


```
kubectl apply -f mypodcrt.yml
```


##### step-4 :- verify the pod's status


```
kubectl get pods
```

##### step-5 :- to verify pod's detail info


```
kubectl get pod pod1 -o wide

```



### How to create pod inside custom namespace ?


##### step-1 :- List all namespaces and if no custom namespaces there , then you create a custom namespaces


A. verify all namespaces


```
kubectl get namespaces
```

OR

```
kubectl get ns
```


B. Create a new custom namespace


```
kubectl create namespace <name>
```


##### step-2 :- create yaml file for pod create


```bash
vi mypodcrt.yml
```


##### step-3 :- use below command for pod create


`A. If it is kubeadm then👇👇`


```
apiVersion: v1
kind: Pod
metadata:
  name: pod1
  namespace: <namespacename>
spec:
  nodeSelector:
    kubernetes.io/hostname: worker-1
  containers:
    - name: container1
      image: nginx
      ports:
        - containerPort: 80

```


`B. If it is minikube then👇👇`


```
apiVersion: v1
kind: Pod
metadata:
  name: pod1
  namespace: <namespacename>
spec:
  containers:
  - name: container1
    image: nginx
    ports:
    - containerPort: 80

```


##### step-4 :- apply the manifest file(mypodcrt.yml) to create the pod


```
kubectl apply -f mypodcrt.yml
```


##### step-5 :- verify the pod's status


```
kubectl get pods
```

##### step-6 :- to verify pod's detail info


```
kubectl get pod pod1 -o wide

```


## ## What is namespace ?


In Kubernetes (k8s), a Namespace is basically a way to divide cluster resources between multiple users or projects.

You can think of it like this :-

  - Imagine Kubernetes as a giant apartment building.
    
  - Each Namespace is like a separate apartment within that building.

  - Inside each apartment (Namespace), you can have your own furniture (Pods, Services, Deployments, etc.) without bothering the neighbors.
    
  - They’re isolated from each other, but still living in the same overall building (the cluster).
    
  - In one namespace, you can have App A  and In another namespace, you can have App B.


    
### Why use Namespaces ?


`Organization :-` Helps separate environments (like dev, staging, production).

`Resource limits :-` You can apply quotas to prevent one team from hogging all the cluster resources.

`Access control :-` You can set up rules so that different teams can only see or modify stuff in their own namespace.


#### note :- 

Kubernetes starts with some built-in namespaces like.

   - default :- Where stuff goes if you don’t specify a namespace.

   - kube-system :- Where k8s system stuff runs (like networking plugins, DNS, etc.).

   - kube-public :- Public stuff available to everyone (rarely used).




### Namespace Commands


1. List all namespaces

```
kubectl get namespaces
```

OR

```
kubectl get ns
```


2. Create a new namespace

```
kubectl create namespace <name>
```


3. Show details about a namespace

```
kubectl describe namespace <name>
```


4. Delete a namespace

```
kubectl delete namespace <name>
```


5. How to set/switch to namespace(default/custom) for your current kubectl session

```
kubectl config set-context --current --namespace=<name>
```

6. How to check what is your current namespace

```
kubectl config view --minify --output 'jsonpath={..namespace}'
```



## ## what is k8s-volume ?


in k8s, when a container crashes or restarts, any data inside it is lost so volumes solve this by providing persistent or shared storage.

k8s volume is a storage resources that containers in a pod can use to store & share data.

unlike the ephemeral storage inside containers, a volume can persist data beyond the containers life.



### how to use k8s-volume ( multiple file = pv, pvc, podusepvc)


##### step-1 :- create a persistent volume(pv)


`vi ourpv.yml`


```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 2Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
  persistentVolumeReclaimPolicy: Retain

```


##### step-2 :- apply persistent volume(pv)


```
kubectl apply -f ourpv.yml
```

##### step-3 :- check persistent volume(pv) status


```
kubectl get pv
```

##### step-4 :- check persistent volume(pv) detailed info


```
kubectl describe pv my-pv
```

##### step-5 :- create a persistent volume claim(pvc)


`vi ourpvc.yml`


```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests: 
      storage: 300Mi

```


##### step-6 :- apply persistent volume claim(pvc)


```
kubectl apply -f ourpvc.yml
```


##### step-7 :- check persistent volume claim(pvc) status


```
kubectl get pvc
```


##### step-8 :- check persistent volume claim(pvc) detailed info


```
kubectl describe pvc my-pvc
```


##### step-9 :- Use pvc in a pod


`vi mypvcuse.yml`


```
apiVersion: v1
kind: Pod
metadata:
  name: pvc-use-pod
spec:
  containers:
  - name: cont1
    image: nginx:latest
    command: [ "sh", "-c", "echo 'hii all i m ram' > /data/mydata.txt && sleep 3600" ]
    volumeMounts:
    - mountPath: /data
      name: my-datastorage
  volumes:
  - name: my-datastorage
    persistentVolumeClaim:
      claimName: my-pvc

```


##### step-10 :- apply pvc in a pod create file


```
kubectl apply -f mypvcuse.yml
```

##### step-11 :- verify pvc is mounted (inside pod)


```
kubectl get pod pvc-use-pod
```

##### step-12 :- go inside pod and check your data


```
kubectl exec -it pvc-use-pod -- sh
```

```
cat /data/mydata.txt
```

OR

```
cd data/
```

```
cat mydata.txt
```



### how to use k8s-volume ( single file)


##### step-1 :- create a file


`vi myk8svoluse.yml`


```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 2Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
  persistentVolumeReclaimPolicy: Retain

---

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests: 
      storage: 300Mi

---

apiVersion: v1
kind: Pod
metadata:
  name: pvc-use-pod
spec:
  containers:
  - name: cont1
    image: nginx:latest
    command: [ "sh", "-c", "echo 'hii all i m ram' > /data/mydata.txt && sleep 3600" ]
    volumeMounts:
    - mountPath: /data
      name: my-datastorage
  volumes:
  - name: my-datastorage
    persistentVolumeClaim:
      claimName: my-pvc

```


##### step-2 :- apply it


```
kubectl apply -f myk8svoluse.yml
```


##### step-3 :- check your pod status


```
kubectl get pod pvc-use-pod
```


##### step-4 :- go inside pod and check your data


```
kubectl exec -it pvc-use-pod -- sh
```

```
cat /data/mydata.txt
```

OR

```
cd data/
```

```
cat mydata.txt
```



### how to delete k8s-volume


##### step-1 :- delete the pod first


```
kubectl delete pod pvc-use-pod
```

```
kubectl get pod
```

##### step-2 :- delete the pvc


```
kubectl delete pvc my-pvc
```

```
kubectl get pvc
```

##### step-3 :- delete the pv now


```
kubectl delete pv my-pv
```

```
kubectl get pv
```






