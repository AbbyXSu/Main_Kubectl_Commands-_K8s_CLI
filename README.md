# Main_Kubectl_Commands_K8s_CLI
## Install hyperhit and minikube
```
brew update
brew install hyperkit
brew install minikube
kubectl
minikube
```


## Create minikube cluster
```
minikube start --vm-driver=hyperkit
kubectl get nodes
minikube status
kubectl version
```

## Delete cluster and restart in debug mode
```
minikube delete
minikube start --vm-driver=hyperkit --v=7 --alsologtostderr
minikube status
```

## Kubectl commands
```
kubectl get nodes
```
```
kubectl get services
```
service exists and bind to an static permanent IP address, in the case of pod crashed, service will spin up/create another pod to support the service with zero down time
```
kubectl get pod
```
pod cannot be created, however, it can be activiated through creating deployment
```
kubectl create deployment Name --images=images [--dry-run] [options]
kubectl create deployment nginx-depl --image=nginx
```
create deployment provide a blueprint for creating pods, with only mention the images and the define the name, it provide basic configuration for the deployment, leaving the rest to default. 
```
kubectl get deployment
```
```
kubectl get replicaset
```
Replicaset is managing the replicas of a pod, it is managed via deployment , the layers of Abstraction is 
Deployment manages a ReplicaSet; 
ReplicaSet manages a Pod;
Pod is an abstraction of an container;
Container and below is managed by K8s directly and automatically upon config using Deployment command

```
kubectl edit deployment nginx-depl
```
This command gives the auto generated configuration file with default values of the deployment nginx-depl

## Debugging
```
kubectl logs {pod-name}
```
shows the application status of the pod,kubectl describe can also show further images events/ status when creating 
```
kubectl exec -it {pod-name} -- bin/bash
```
This create a n interactive terminal of the application container as a root user to test or execute command there
Examples:
```
create mongo deployment
kubectl create deployment mongo-depl --image=mongo
kubectl logs mongo-depl-{pod-name}
kubectl describe pod mongo-depl-{pod-name}
```

## Delete deplyoment
```
kubectl delete deployment [deployment name]
kubectl delete deployment mongo-depl
kubectl delete deployment nginx-depl
```
After deleting, can confirm deletion using get replicaset, get deployment or get pod

## Create or edit config file
```
vim nginx-deployment.yaml
kubectl apply -f nginx-deployment.yaml
kubectl get pod
kubectl get deployment
```
using yaml config file to execute deployment is more common instead of using line by line commands 
amending the yaml file after creating the deployment is possible as K8s will detect if the deploymemt has already exists and will be able to update it if it already exists.

## Delete with config
```
kubectl delete -f nginx-deployment.yaml
```
## Metrics
```
kubectl top 
```
The kubectl top command returns current CPU and memory usage for a cluster’s pods or nodes, or for a particular pod or node if specified
