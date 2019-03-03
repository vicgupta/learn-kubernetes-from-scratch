# Deploy simple nginx

### Deploy the nginx using deployment 
```
kubectl create deployment nginx --image=nginx:alpine
```
### Create service or expose the deployment
```
kubectl expose deployment nginx --type NodePort --port 80
```
## See the details of the deployment
```
kubectl describe deployment nginx
```
### See the details of the service
```
kubectl describe service nginx
```
### Scale the deployments to 6 replicas
```
kubectl scale deployment nginx --replicas=6
```
### See the details of the pods
```
kubectl get pods
```
### Destroy and delete the service and deployment
```
kubectl delete svc nginx && kubectl delete deployment nginx
```
