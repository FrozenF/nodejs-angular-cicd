## TEMPLATE HELM CHART

### Pre-Requisite
1. Namespace
```
kubectl create ns <namespace>
```
2. Image Secret
```
kubectl -n <namespace> create secret docker-registry <secret-name> \ 
    --docker-server=<harbor-registry-server> \
    --docker-username=<harbor-username> \
    --docker-password=<harbor-password>
```

3. Database Secret
```
kubectl -n <namespace> create secret generic db-secret \
    --from-literal=DB_HOST=<database-host> \
    --from-literal=DB_NAME=<database-name> \
    --from-literal=DB_USER=<database-user> \
    --from-literal=DB_PASS=<database-pass> 
```
(Optional)
4. TLS Secret
```
kubectl -n <namespace> create secret tls <tls-secret-name> \
    --cert=<cert-file-path> \
    --key=<private-key-path>
```
### Configure Files
1. Configure `volumeMounts` in `templates/nginx-svc-deployment.yaml` as needed by application
2. Configure `volumeMounts` in `templates/php-svc-deployment.yaml` as needed by application
3. (Optional) Configure templates/nginx-configmap.yaml


### Configure values.yaml
Configure values both in development and production match as your settings
1. `environments/development/values.yaml`
2. `environments/production/values.yaml`
