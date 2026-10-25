# Exercise 10: Minikube Multi-Node Multi-App Deployment

## Objective
Set up a multi-node Minikube cluster and deploy multiple application replicas across the cluster.

## Prerequisites
- Docker
- Minikube
- kubectl

## 1. Start a Two-Node Cluster

```bash
minikube start --nodes 2 -p multinode-demo
```

## 2. Verify the Cluster Nodes

```bash
kubectl get nodes
```

Confirm that the cluster nodes are in the `Ready` state.

## 3. Deploy Nginx

```bash
kubectl create deployment nginx --image=nginx
```

## 4. Scale the Deployment

```bash
kubectl scale deployment nginx --replicas=4
```

## 5. Verify the Deployment

```bash
kubectl get deployments
kubectl get pods -o wide
```

Check that four Nginx pods are running and inspect the `NODE` column to see where Kubernetes scheduled them.

**Note:** Kubernetes scheduling does not guarantee that replicas will be evenly distributed across nodes. The actual placement depends on scheduling constraints and cluster resources.

## 6. Cleanup

```bash
kubectl delete deployment nginx
minikube delete -p multinode-demo
```

## Expected Outcome
A two-node Minikube cluster with an Nginx deployment scaled to four replicas. The pod listing shows the node assigned to each replica.