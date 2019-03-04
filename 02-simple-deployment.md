# Start with a simple deployment

### Deploy an nginx web server using container
```
kubectl create deployment nginx --image=nginx:alpine
```
### View the pods that are created
```
kubectl get pods
```
### Use expose to create a service for the deployment
```
kubectl expose deployment nginx --port=80 --type=NodePort
```
### View the service to see which port was the node expsosed on 
```
kubectl describe service nginx
```
Typically this port is greater than 32K+ range.  Look for the line which has NodePort and http into the server (or IP) with the nodeport.  So if the NodePort is at 32373, then http://<ip address>:32373.