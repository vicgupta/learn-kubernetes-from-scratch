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
### You may run minikube instead of kubeadm
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube && sudo cp minikube /usr/local/bin && rm minikube
```
More on minikube on the [kubernetes.io minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/) page.
