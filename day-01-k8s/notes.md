# Day 1 – Kubernetes Basics
 
## What is Kubernetes?

### Definition:
Kubernetes is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications.

### DevOps meaning:
Kubernetes is the platform DevOps teams use to run applications reliably in production without manually managing containers.

### Why it exists:
Docker can run containers, but it cannot manage large-scale applications, handle failures, or scale automatically. Kubernetes solves these problems.

---

## What is `kubectl`?

### Definition:
`kubectl` is the command-line tool used to interact with a Kubernetes cluster.

### DevOps meaning:
`kubectl` is the remote control DevOps engineers use to deploy, update, and debug applications running on Kubernetes.

### Why it exists:
Directly accessing cluster components is unsafe. `kubectl` provides a controlled and secure way to communicate with the Kubernetes API Server.

---

## What is a Kubernetes Cluster?

### Definition:
A Kubernetes cluster is a set of machines that work together to run containerized applications.

### DevOps meaning:
A cluster represents an environment such as development, staging, or production.

### Why it exists:
Applications must run across multiple machines for reliability, scalability, and fault tolerance.

---

## What is a Node?

### Definition:
A node is a machine (virtual or physical) that runs containerized workloads in a Kubernetes cluster.

### DevOps meaning:
In cloud environments, a node is usually a virtual machine like an EC2 instance that DevOps teams manage for capacity and cost.

### Why it exists:
Containers need compute resources (CPU, memory). Nodes provide those resources.

---

## What is a Pod?

### Definition:
A Pod is the smallest deployable unit in Kubernetes and represents one or more containers running together.

### DevOps meaning:
A Pod is a temporary execution unit, not a production deployment object.

### Why it exists:
Some applications need tightly coupled containers (for example, a main app and a sidecar). Pods allow them to run together.
  
---

## Why Pods are NOT used directly in production

### Definition:
Standalone Pods do not have a controller managing them.

### DevOps meaning:
If a Pod crashes or is deleted, Kubernetes will not recreate it automatically.

### Why it matters:
Production systems require self-healing and high availability, which Pods alone cannot provide.

---

## What is a Controller? (Important)

### Definition:
A controller is a Kubernetes component that continuously monitors resources and ensures the desired state is maintained.

### DevOps meaning:
Controllers are the reason Kubernetes can self-heal applications.

### Why it exists:
Without controllers, Kubernetes would not be able to automatically recover from failures.

---

## How a Pod is Created (Observed in Practice)

When I applied the Pod YAML using `kubectl apply`, Kubernetes created the Pod through the following steps:

- kubectl sent the YAML definition to the Kubernetes API Server
- The API Server validated and stored the desired state
- The scheduler selected a node for the Pod
- The kubelet on the node pulled the container image
- The container runtime created and started the container
- The Pod status changed to Running once the container started successfully

---

## Pod Behavior When Deleted (Hands-On Observation)

- When the Pod was deleted manually, Kubernetes did not recreate it
- This confirmed that standalone Pods do not provide self-healing
- Kubernetes only recreates resources that are managed by controllers

---

## Kubernetes commands used (Day 1)
```bash
kubectl get nodes
kubectl get pods
kubectl describe pod
kubectl apply -f pod.yaml
kubectl delete pod
```

---

## Key Takeaways (Day 1)
- Kubernetes does not care about individual resources.
- Kubernetes only enforces the desired state defined by controllers.
