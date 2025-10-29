# Setup steps
### Install Helm  
- [Install Helm](https://helm.sh/docs/intro/install/)
- https://github.com/bitnami/charts/tree/main/bitnami/postgresql


### Pre Deploy
ADD Binami Repository  

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```
```bash
helm repo update
```


Create a values.yaml
```yaml
image:
    debug: true

global:
  postgresql:
    auth:
      postgresPassword: ""

primary:
  resources:
    requests:
      memory: 4Gi
      cpu: 1000m
    limits:
      memory: 8Gi
      cpu: 2000m

readReplicas:
  resources:
    requests:
      memory: 4Gi
      cpu: 1000m
    limits:
      memory: 8Gi
      cpu: 2000m
```
Switch namespace  
```bash
kubectl-ns <your-namespace>
```



### Deploy
```bash
helm install postgresql oci://registry-1.docker.io/bitnamicharts/postgresql --version 16.7.27 -f values.yaml --namespace <your-namespace> \
  --set-string global.postgresql.auth.postgresPassword="postgres_password"
```

### Update
```bash
helm upgrade  postgresql oci://registry-1.docker.io/bitnamicharts/postgresql --version 16.7.27 -f values.yaml  --namespace <your-namespace>
```

### Verify Deployment

Check pods  
```bash
kubectl get pods
```

Check services
```bash
kubectl get svc 
```

### Acess PostgresQL

Get credentials
```bash
kubectl get secret --namespace <your-namespace> postgresql -o jsonpath="{.data.postgres-password}" | base64 -d
```





### Cleanup
```bash
helm uninstall postgresql
kubectl get pvc
kubectl delete pvc data-postgresql-primary-0  data-postgresql-read-0
```