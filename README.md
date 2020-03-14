## Create a namespace
```
kubectl create ns logging
```

## Download helm chart dependencies
```
helm dependency update ./logging
```

## Install helm chart
```
helm install ops-logging ./logging -n logging
```

## Delete ClusterRole and ClusterRoleBinding if it already exists
```
kubectl delete ClusterRole ops-logging-fluentd
kubectl delete ClusterRoleBinding ops-logging-fluentd
```