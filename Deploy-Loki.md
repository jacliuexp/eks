### Loki
```
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
helm pull grafana/loki  # -> loki-5.36.0.tgz
tar -zxvf loki-5.36.0.tgz
cd loki
# copy over values-dev.yaml
```
```
loki:
 auth_enabled: false
 storage:
   bucketNames:
     chunks: dev-chunks
     ruler: dev-ruler
     admin: dev-admin1
   s3:
     endpoint: null
     region: us-east-1
minio:
```
##### Issue
```
myloki->charts->loki->charts->minio+grafana-agent-operator
myloki: helm template -f values-dev.yaml . | grep minio   # still show minio due to charts->loki->charts->minio+grafana...
copy over values-dev.yaml to loki (loki->charts->minio+grafana-agent-operator): loki: helm template -f values-dev.yaml . | grep minion # minio doesn't show
```


