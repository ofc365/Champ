# minikube-proj


step-1 :- create ubuntu instance

step-2 :- install docker

step-3 :- install minikube and kubectl

step-4 :- `eval $(minikube docker-env)`

step-5 :- create `Dockerfile`

```
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

step-6  :- create `index.html`

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



step-7 :- Build image , tag and push


`docker build -t minikube-img:latest .`


step-8 :- create `deployment.yaml`

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

step-9 :- Apply it `kubectl apply -f deployment.yaml` &  `minikube service html-app-service`

step-10 :- Test it `ssh -i "key-name" -L 30000:192.168.49.2:30000 ubuntu@ec2-pub-ip`

------------------------------------------------
