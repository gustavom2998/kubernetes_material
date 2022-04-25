
# KubeCTL

Getting started with Kubectl.

## Kubernetes Components

```bash
# kubectl get nodes | pod | services | replicaset | deployment (Components)
kubectl get nodes 

kubectl get pods 

kubectl get deployment
```

## CRUD for deployments

```bash
kubectl create deployment mongo-depl --image=mongo # Create a mongo deployment (CRUD)

kubectl edit deployment mongo-depl # Edit the mongo deployment (CRUD)

kubectl delete deployment mongo-depl # Delete mongo deployment (CRUD)
```

## Debugging Pods

```bash
kubectl logs mongo-depl-85ddc6d66-g7x6b # Get logs for mongo deployment (Logging)

kubectl describe mongo-depl-85ddc6d66-g7x6b # get description for Mongo pod (Components - Container setup)

kubectl exec -it mongo-depl-85ddc6d66-g7x6b -- bin/bash # Open mongo deployment interactive terminal (Terminal)
```

## Configuration Files

```bash
kubectl apply -f nginx-deployment.yml # Create Deployment with configuration file (Configuration file)

kubectl delete -f nginx-delete.yml # Delete Deployment with configuration file (Configuration file)
```
