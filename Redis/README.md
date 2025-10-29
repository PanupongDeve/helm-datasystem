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
helm install redis oci://registry-1.docker.io/bitnamicharts/redis --version 23.2.2 -f values.yaml  -n redis --set auth.password='password'
```


### Cleanup
```bash
kubens redis
kubectl delete -f ./redis-np.yaml
helm uninstall redis
kubectl get pvc
kubectl delete pvc redis-data-redis-master-0  redis-data-redis-replicas-0
```


### Client Tools
Name: Redis insight  
Source: https://redis.io/downloads 

