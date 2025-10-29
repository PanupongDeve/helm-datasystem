# Install Redis with helm #

1. Add helm repo bitnami
```
helm repo add bitnami https://charts.bitnami.com/bitnami
```

2. Update helm repo
```
helm repo update
```


3. Create namespace for redis
```
kubectl create ns redis
```

4. Install redis Pod=1

Find version redis: https://artifacthub.io/packages/helm/bitnami/redis  


```
helm install redis oci://registry-1.docker.io/bitnamicharts/redis -n redis --set redis.password='password' --set replica.replicaCount=1
```