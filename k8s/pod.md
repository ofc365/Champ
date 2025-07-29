## How to create pod inside default namespace ?


```
vi mypodcrt.yml
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
kubectl apply -f mypodcrt.yml
```

```
kubectl get pods
```

```
kubectl get pod pod1 -o wide

```



### How to create pod inside custom namespace ?



```
kubectl create namespace <name>
```

```
kubectl get ns
```


```
vi mypodcrt.yml
```


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


```
kubectl apply -f mypodcrt.yml
```


--------------------------------------------------
