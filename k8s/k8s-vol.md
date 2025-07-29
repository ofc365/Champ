## how to use k8s-volume



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


```
kubectl apply -f myk8svoluse.yml
```


```
kubectl get pod pvc-use-pod
```


#### go inside pod and check your data


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



------------------------------------------------------
