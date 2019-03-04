#  Start an nginx deployment

### Let's start with a nginx deployment
```
kubectl apply -f https://k8s.io/examples/application/deployment.yaml
```
### Get the details of the deployment
```
kubectl describe deployment nginx-deployment
```
### Lookup all the pods using kubectl
```
kubectl get pods
```
### Update the nginx deployment
```
kubectl apply -f https://k8s.io/examples/application/deployment-update.yaml
```
### Scale the replicas to 4
```
kubectl apply -f https://k8s.io/examples/application/deployment-scale.yaml
```
### Lookup all the pods using kubectl
```
kubectl get pods
```
### Ready to delete the deployment
```
kubectl delete deployment nginx-deployment
```
