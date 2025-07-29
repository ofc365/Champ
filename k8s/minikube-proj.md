# minikube-proj


create instance ; install docker, minikube and kubectl

```
eval $(minikube docker-env)
```

vi Dockerfile

```
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

vi index.html

```
<html>
<head>
    <title>minikube webapp</title>
</head>
<body>
    <h1>Welcome to minikube webapp!</h1>
</body>
</html>
```

Build image , tag and push


`docker build -t minikube-img:latest .`


vi deployment.yaml

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: html-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: html-app
  template:
    metadata:
      labels:
        app: html-app
    spec:
      containers:
      - name: html-app
        image: IMG-NAME:TAG
        ports:
        - containerPort: 80

---
apiVersion: v1
kind: Service
metadata:
  name: html-app-service
spec:
  type: NodePort
  selector:
    app: html-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
    nodePort: 30000
```


```
kubectl apply -f deployment.yaml
```

```
minikube service html-app-service
```

Test it : `ssh -i "key-name" -L 30000:192.168.49.2:30000 ubuntu@ec2-pub-ip`

`localhost:30000`


------------------------------------------------
