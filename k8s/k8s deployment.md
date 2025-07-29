## How to create k8s deployment file 


`vi mydeployment.yml`


```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mynginx-deployment
  labels:
    app: myapp
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: appcontainer
        image: nginx:latest
        ports:
        - containerPort: 80

```


```
kubectl apply -f mydeployment.yml
```

```
kubectl get deployments
```


```
kubectl get pods
```

```
kubectl describe pod <pod-name>
```

For scale `kubectl scale deployment --replicas=5 myapp`


---------------------------------------------------------------
