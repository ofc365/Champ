## How to create pod inside default namespace ?


```
vi default-namespace-pod-crt.yml
```


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


```
kubectl apply -f default-namespace-pod-crt.yml
```

```
kubectl get pods
```

```
kubectl get pod pod1 -o wide

```



### How to create pod inside custom namespace ?



```
kubectl create namespace custons
```

```
kubectl get ns
```


```
vi custom-namespace-pod-crt.yml
```


```
apiVersion: v1
kind: Pod
metadata:
  name: pod2
  namespace: custons
spec:
  containers:
  - name: container2
    image: nginx
    ports:
    - containerPort: 81

```


```
kubectl apply -f mypodcrt.yml
```


--------------------------------------------------
