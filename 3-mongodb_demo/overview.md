# Deploying Mongo with Kubernetes

The objective of this project is to:

- Create a MongoDB pod
- Create a MongoDB service to talk to the pod
- The service must be internal (only requests from the same server)
- Create a Mongo express deployment
    - Database URL of the MongoDb
    - Credentials so we can authenticate
    - Passed through env vars with the config map
    - Secret with credentials
    - Config file referencing the config map and the secret
- Open Mongo Express to access through the browser with an external service

Request flow:
1. Browser
2. Mongo Express External Service
3. Mongo Express Pod
4. Mongo DB Internal Service
5. MongoDB Pod

## Development

```bash
# Create the secret first - so the deployment works
kubectl apply -f 3-mongodb_demo/mongodb-secret.yml 

# Check the secret was created
kubectl get secret

# Create the deployment referencing the secret
kubectl apply -f 3-mongodb_demo/mongodb-deployment.yml

# Wait for pod to create
kubectl get pod --watch

# Append the MongoDB internal service and update the deployment
kubectl apply -f 3-mongodb_demo/mongodb-deployment.yml

# Check the service was created
kubectl get services

# Check the service is attached to the correct pod - 172.17.0.3:27017
kubectl describe service mongodb-service

# Check that the IP from the previous command matches the pod IPs - 172.17.0.3
kubectl get pods -o wide

# Create the config map with the database name and url
kubectl apply -f 3-mongodb_demo/mongodb-configmap.yml

# Create the mongoexpress deployment
kubectl apply -f 3-mongodb_demo/mongoexpress-deployment.yml

# Append the Mongo Express external service and update the deployment
kubectl apply -f 3-mongodb_demo/mongoexpress-deployment.yml

# Create tunnel in other shell (https://github.com/kubernetes/minikube/issues/13823) - ip from tunnel http://172.31.28.98:30000/
minikube tunnel

## Assign a public IP adress for the external service (Since it's pending)
minikube service mongo-express-service 

# Get the external ip for mongo-express-service (10.100.126.225:30000/)
kubectl get service
```
