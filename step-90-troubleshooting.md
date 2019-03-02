# How to troubleshoot

### If you forgot on the token from kubeadm and don't know how to join the nodes, you can lookup the command
```
kubeadm token create --print-join-command
```
### If you want the Kubernetes dashboard
```
kubectl create -f https://raw.githubusercontent.com/kubernetes/dashboard/master/aio/deploy/recommended/kubernetes-dashboard.yaml
```
### If you want to install flannel instead of weave
```
sudo kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```
### If you want to install kube-bench - for seeing the configuration pass/fail of the kubernetes
```
docker run --rm -v `pwd`:/host aquasec/kube-bench:latest install
```
You then use ```./kube-bench server``` to run the script
