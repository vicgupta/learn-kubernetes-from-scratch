# Start with a simple deployment

### Deploy an nginx web server using container
```
kubectl create deployment nginx --image=nginx:alpine
```
### View the pods that are created
```
kubectl get pods
```
### Add more replicas (or more number of pods) to your deployment
```
kubectl scale deployment nginx replicas=2
```