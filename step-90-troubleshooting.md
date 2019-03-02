# How to troubleshoot

### If you forgot on the token from kubeadm and don't know how to join the nodes, you can lookup the command
```
kubeadm token create --print-join-command
```
### If you want the Kubernetes dashboard
```
kubectl create -f https://raw.githubusercontent.com/kubernetes/dashboard/master/aio/deploy/recommended/kubernetes-dashboard.yaml
```

