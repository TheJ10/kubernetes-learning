# Day 2 – Deployments, ReplicaSets & Scaling

## What is a Deployment?

### Definition:
A Deployment is a Kubernetes resource that manages Pods by ensuring the desired number of replicas are running at all times.

### DevOps meaning:
A Deployment is the primary Kubernetes resource DevOps teams use to run and manage applications in production with self-healing and controlled scaling.

### Why it exists:
Standalone Pods do not self-heal. If a Pod crashes or is deleted, it does not come back automatically. Deployments solve this problem by continuously monitoring and maintaining Pods.

---

## What is a ReplicaSet?

### Definition:
A ReplicaSet is a Kubernetes resource that ensures a specified number of identical Pods are running.

### DevOps meaning:
ReplicaSets are used by Kubernetes internally to ensure the correct number of Pods are running, but DevOps teams usually manage them indirectly through Deployments.

### Why it exists:
Kubernetes needs a mechanism to maintain availability. ReplicaSets provide this by enforcing the desired number of Pods.

> Note: In practice, DevOps engineers rarely create ReplicaSets directly. They are automatically created and managed by Deployments.

---

## Relationship Between Deployment, ReplicaSet, and Pod

- A Deployment defines the desired state (for example, 2 replicas)
- The Deployment creates and manages a ReplicaSet
- The ReplicaSet creates and manages Pods
- Pods run the actual application containers

This separation allows Kubernetes to provide self-healing and scaling.

---

## Self-Healing in Kubernetes (Observed Behavior)

### What self-healing means:
Self-healing is Kubernetes’ ability to automatically recover from failures without manual intervention.

### What was observed in practice:
- When a Pod created by a Deployment was deleted manually
- The ReplicaSet detected that the actual number of Pods was less than desired
- A new Pod was created automatically
- The application continued running without downtime

This behavior is critical for production systems.

---

## Scaling in Kubernetes

### What scaling means:
Scaling is the process of increasing or decreasing the number of Pods running an application.

### How scaling works:
- Scaling is done by changing the desired replica count
- Kubernetes does not scale containers directly
- The Deployment updates the ReplicaSet
- The ReplicaSet creates or deletes Pods to match the desired state

---

## Scaling Observations (Hands-On)

- Scaling up increased the number of Pods running the application
- Scaling down reduced the number of Pods safely
- Kubernetes handled Pod creation and deletion automatically
- The application remained stable during scaling

---

## Code vs Live Cluster State (Important Concept)

- The YAML file represents the desired state stored in code (Git)
- Commands like `kubectl scale` modify the live cluster state only
- The YAML file does not change automatically
- To make scaling permanent, the replica count must be updated in the YAML and reapplied

This separation allows safe operational changes without immediately modifying code.

---

## Kubernetes Commands Used (Day 2)
```bash
kubectl apply -f deployment.yaml
kubectl get deployments
kubectl get rs
kubectl get pods
kubectl scale deployment
kubectl delete pod
```

---

## Key Takeaways (Day 2)

- Deployments are the standard way to run applications in Kubernetes
- ReplicaSets enforce the desired number of Pods
- Self-healing is achieved through controllers
- Scaling is achieved by updating desired state, not by manually creating Pods
