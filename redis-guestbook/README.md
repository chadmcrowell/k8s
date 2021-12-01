# Example Guestbook Application with Redis Backend and PHP Frontend

- [source](https://kubernetes.io/docs/tutorials/stateless-application/guestbook/)

---

## Create the Redis Leader Deployment
Create a deployment in Kubernetes with the following command:
```bash
kubectl apply -f deploy-redis-leader.yml
```
List the deployments and pods as a result of the previous command:
```bash
kubectl get deploy,po
```
Optionally view the logs from the redis leader pod:
```bash
kubectl logs -f deployment/redis-leader
```

## Create the Redis Leader Service
To allow communication from the frontend to the backend leader, create this kubernetes service:
```bash
kubectl apply -f svc-leader.yml
```
List the services as a result of the previous command:
```bash
kubectl get svc
```

## Create the Redis Follower Deployment
In order to create redundancy and scale for your redis database, you can create additional follower pods by creating this deployment:
```
kubectl apply -f deploy-redis-follower.yml
```
List the deployment and pods as a result of the previous command:
```
kubectl get deploy,po
```

## Create the Redis Follower Service
To allow communication from the frontend to the backend follower pods, create this kubernetes service:
```bash
kubectl apply -f svc-follower.yml
```
List the services as a result of the previous command:
```bash
kubectl get svc
```

## Create the Frontend Deployment
This application has a PHP frontend, exposing a JSON interface and serves a JQuery-Ajax-based UX. Create the frontend by creating this deployment:
```bash
kubectl apply -f deploy-frontend.yml
```
List the pods as a result of the previous command, filtering by label:
```bash
kubectl get po -l app=guestbook -l tier-frontend
```

## Create the Frontend Service
In order for guests to access the guestbook, create a service:
```bash
kubectl apply -f svc-frontend.yml
```
List the services as a result of the previous command:
```bash
kubectl get svc
```
