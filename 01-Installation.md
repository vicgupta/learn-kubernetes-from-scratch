# Installation using VM images on Ubuntu Xenial 16.04 Minimal

## Step 1 - Install all the components using the command line interface

## Install a new network
```
gcloud compute networks create learn-kubernetes-from-scratch --subnet-mode custom
```
## Install a new subnet
```
gcloud compute networks subnets create kubernetes-subnet \
  --network learn-kubernetes-from-scratch \
  --range 10.1.0.0/24
```
##  Install new firewall rules for internal
```
gcloud compute firewall-rules create learn-kubernetes-from-scratch-allow-internal \
  --allow tcp,udp,icmp \
  --network learn-kubernetes-from-scratch \
  --source-ranges 10.1.0.0/24,10.20.0.0/16
```
## Install new firewall rules to external
```
gcloud compute firewall-rules create learn-kubernetes-from-scratch-allow-external \
  --allow tcp:22,tcp:6443,icmp,tcp:80,tcp:443 \
  --network learn-kubernetes-from-scratch \
  --source-ranges 0.0.0.0/0
```
## List the firewall rules
```
gcloud compute firewall-rules list --filter="network:learn-kubernetes-from-scratch"
```
## Set the region and zone
```
gcloud config set compute/region us-west1
gcloud config set compute/zone us-west1-c
```
## Create the asociation
```
gcloud compute addresses create learn-kubernetes-from-scratch \
  --region $(gcloud config get-value compute/region)
```
## List the addresses
```
gcloud compute addresses list --filter="name=('learn-kubernetes-from-scratch')"
```
## Install the controller or master nodes
```
for i in 0 1 2; do
  gcloud compute instances create kubernetes-controller-${i} \
    --async \
    --boot-disk-size 10GB \
    --can-ip-forward \
    --image-family ubuntu-1604-lts \
    --image-project ubuntu-os-cloud \
    --machine-type n1-standard-1 \
    --private-network-ip 10.1.0.1${i} \
    --scopes compute-rw,storage-ro,service-management,service-control,logging-write,monitoring \
    --subnet kubernetes-subnet \
    --tags learn-kubernetes-from-scratch,controller
done
```
## Install the worker nodes
```
for i in 0 1 2; do
  gcloud compute instances create kubernetes-worker-${i} \
    --async \
    --boot-disk-size 10GB \
    --can-ip-forward \
    --image-family ubuntu-1604-lts \
    --image-project ubuntu-os-cloud \
    --machine-type n1-standard-1 \
    --private-network-ip 10.1.0.2${i} \
    --scopes compute-rw,storage-ro,service-management,service-control,logging-write,monitoring \
    --subnet kubernetes-subnet \
    --tags learn-kubernetes-from-scratch,worker
done
```
