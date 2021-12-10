### Run redis cluster in k8s: </br>
-------------------------------------------
```
kubectl apply -f - <<EOF
apiVersion: v1
kind: PersistentVolume
metadata:
  name: redis-etc-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Retain
  nfs:
    server: 10.10.1.226
    path: /var/redis_etc_pv
EOF
```
---------------------------------------------
```
kubectl apply -f - <<EOF
apiVersion: v1
kind: PersistentVolume
metadata:
  name: redis-data-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Retain
  nfs:
    server: 10.10.1.226
    path: /var/redis_data_pv
EOF
```
---------------------------------------------
```
kubectl apply -f - <<EOF
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: redis-data-pvc
spec:
  accessModes:
  - ReadWriteMany
  resources:
    requests:
      storage: 1Gi
  volumeName: redis-data-pv
EOF
```
---------------------------------------------
```
kubectl apply -f - <<EOF
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: redis-etc-pvc
spec:
  accessModes:
  - ReadWriteMany
  resources:
    requests:
      storage: 1Gi
  volumeName: redis-etc-pv
EOF
```
---------------------------------------------
```
kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: redis-pod
  labels:
    name: redis-pod-lbl
spec:
  containers:
  - name: redis
    image: redis:latest
    imagePullPolicy: IfNotPresent
    ports:
    - name: nginx
      containerPort: 6379
      protocol: TCP
    volumeMounts:
    - name: redis-etc-store
      mountPath: /opt/redis/etc
    volumeMounts:
    - name: redis-data-store
      mountPath: /opt/redis/data
  volumes:
  - name: redis-etc-store
    persistentVolumeClaim:
       claimName: redis-etc-pvc
  volumes:
  - name: redis-data-store
    persistentVolumeClaim:
       claimName: redis-data-pvc
EOF
```
-------------------------------------------
```
kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: redis-pod
  labels:
    name: redis-pod-lbl
spec:
  containers:
  - name: redis
    image: redis:latest
    imagePullPolicy: IfNotPresent
    ports:
    - name: nginx
      containerPort: 6379
      protocol: TCP
EOF
````



---
work notes: </br>
Конфиги и data в redis docker image: [https://hub.docker.com/_/redi](https://hub.docker.com/_/redis) </br>
