
# Install kubernetes components using Kubeadm
Install various components of Kubernetes like docker, kubeadm, kubelet, kubectl on Ubuntu (bionic 18.04 or xenial 16.04).

### Using git repositories in a single command
```
sudo apt update && sudo apt install -y git && git clone http://github.com/vicgupta/xenial-shell && cd xenial-shell && bash kubeadm.sh
```
### Configure Kubeadm and associated Kubernetes components
```
sudo kubeadm init
```
### Configure to ensure you can run the kubectl
```
mkdir -p $HOME/.kube && sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config && sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
### Run Weave as the network overlay
```
kubectl apply -n kube-system -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 |tr -d '\n')"
```
### Run taint on the master so that it can be used as worker
```
kubectl taint node $(hostname) node-role.kubernetes.io/master:NoSchedule-
```
### Check if all
```
kubectl get pods --all-namespaces
```
