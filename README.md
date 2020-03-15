# Logging

## Setup
## 1. Create a namespace
```
kubectl create ns logging
```
## 2. Download helm chart dependencies
```
helm dependency update ./logging
```
## 3. Install helm chart
```
helm install ops-logging ./logging -n logging
```

## Delete
### 4. namespace
```
kubectl delete ns logging
```
### 5. ClusterRole and ClusterRoleBinding if it already exists for logging
```
kubectl delete ClusterRole ops-logging-fluentd
kubectl delete ClusterRoleBinding ops-logging-fluentd
```

# Metrics

## Setup
### 1. Create a namespace
```
kubectl create ns metrics
```
### 2. Download helm chart dependencies
```
helm dependency update ./metrics
```
### 3. Install helm chart
```
helm install ops-metrics ./metrics/ --render-subchart-notes -n metrics
```

## Accessing prometheus and graphana
### 1. Graphana Dashboard
```
kubectl get secret ops-metrics-grafana -n metrics -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
export POD_NAME=$(kubectl get pods -n metrics -l "app.kubernetes.io/name=grafana" -o jsonpath="{.items[0].metadata.name}")
kubectl -n metrics port-forward $POD_NAME 3000
```
### 1. Prometheus Dashboard
```
export POD_NAME=$(kubectl get pods -n metrics -l "app=prometheus,component=server" -o jsonpath="{.items[0].metadata.name}")
kubectl -n metrics port-forward $POD_NAME 9090
```


## Delete
### 4. namespace 
```
kubectl delete ns metrics
```
### 5. ClusterRole and ClusterRoleBinding if it already exists for metrics
```
kubectl delete PodSecurityPolicy ops-metrics-grafana
kubectl delete PodSecurityPolicy ops-metrics-grafana-test
kubectl delete PodSecurityPolicy ops-metrics-prometheus-redis-exporter
kubectl delete ClusterRole ops-metrics-prometheus-pushgateway
kubectl delete ClusterRole ops-metrics-grafana-clusterrole
kubectl delete ClusterRole ops-metrics-prometheus-server
kubectl delete ClusterRole ops-metrics-prometheus-alertmanager
kubectl delete ClusterRole ops-metrics-kube-state-metrics
kubectl delete ClusterRoleBinding ops-metrics-grafana-clusterrolebinding
kubectl delete ClusterRoleBinding ops-metrics-kube-state-metrics
kubectl delete ClusterRoleBinding ops-metrics-prometheus-alertmanager
kubectl delete ClusterRoleBinding ops-metrics-prometheus-pushgateway
kubectl delete ClusterRoleBinding ops-metrics-prometheus-server
<<<<<<< HEAD
```

=======
```
>>>>>>> 9206a3c5fb3b75e1416ff2515211f2f3a8e35039
