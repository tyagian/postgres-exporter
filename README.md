
# Postgres exporter

# Steps to deploy: 

1. Add helm repo on jumphost
```helm repo add  ```

2. Check if secret is created before deploying postgres exporter. Use this to create secret with multiple database. If secret is not available, create secret with this command: 

```
kubectl create secret generic postgres-exporter --from-literal=DATA_SOURCE_NAME='postgresql://<user>:<pass>@aws-aurora-postgresql11-qa.cluster-crbt0lofm6sv.us-west-2.rds.amazonaws.com:5432/qa?sslmode=require,postgresql://<user>:<pass>@aws-aurora-postgresql11-dev.cluster-crbt0lofm6sv.us-west-2.rds.amazonaws.com:5432/dev?sslmode=require,postgresql://<user>:<pass>@aws-aurora-postgresql11-cm.cluster-crbt0lofm6sv.us-west-2.rds.amazonaws.com:5432/cm?sslmode=require,postgresql://<user>:<pass>@pg-plan-network-qa.cluster-crbt0lofm6sv.us-west-2.rds.amazonaws.com:5432/qa?sslmode=require,postgresql://<user>:<pass>@pg-plan-network-cm.cluster-crbt0lofm6sv.us-west-2.rds.amazonaws.com:5432/cm?sslmode=require' -n prometheus
```

3. Deploy postgres exporter using helm file
```
helm install postgres-exporter prometheus-community/prometheus-postgres-exporter -f values.yaml -n prometheus
```

4. Validate pod logs and status. If any database connection get failed or any query is incorrect, pod may show running status but logs will show errors. 


Resource url: https://github.com/prometheus-community/helm-charts/tree/main/charts/prometheus-postgres-exporter
