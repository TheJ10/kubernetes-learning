# Day 3 – Kubernetes Services

## What is a Service?

### Definition:
A Service is a Kubernetes resource that provides a stable network endpoint to access a group of Pods.

### DevOps meaning:
Services are used by DevOps and cloud teams to expose applications reliably, even when Pods are recreated, scaled, or replaced.

### Why it exists:
Pods are temporary and their IP addresses change frequently. Services solve this problem by providing a stable IP and DNS name.

---

## Why Pods Cannot Be Accessed Directly

### Definition:
Pods are ephemeral Kubernetes objects whose lifecycle is controlled by controllers.

### DevOps meaning:
Directly exposing Pods is unreliable because they can be deleted, recreated, or moved across nodes at any time.

### Why it exists:
Kubernetes is designed for dynamic workloads. Networking must adapt automatically to these changes.

---

## How Services Work Internally

### Definition:
Services use labels and selectors to dynamically discover Pods.

### DevOps meaning:
A Service does not know Pod IPs in advance. It continuously selects Pods based on labels and routes traffic to them.

### Why it exists:
This design allows applications to scale and self-heal without breaking network connectivity.

---

## What are Endpoints?

### Definition:
Endpoints are Kubernetes objects that store the list of Pod IPs backing a Service.

### DevOps meaning:
Endpoints represent the real-time backend targets for a Service and are automatically updated as Pods change.

### Why it exists:
Without Endpoints, Services would not know where to send traffic.

---

## NodePort Service

### Definition:
A NodePort Service exposes an application on a fixed port of each node in the cluster.

### DevOps meaning:
NodePort is mainly used for local development, demos, and learning purposes.

### Why it exists:
It provides a simple way to access applications from outside the cluster without advanced networking components.

---

## ClusterIP Service

### Definition:
A ClusterIP Service exposes an application only within the Kubernetes cluster.

### DevOps meaning:
ClusterIP is the most commonly used Service type for internal communication between microservices.

### Why it exists:
Most applications should not be publicly accessible. ClusterIP provides secure internal networking by default.

---

## ClusterIP vs NodePort (Comparison)

- ClusterIP is internal-only and used in production environments
- NodePort exposes applications externally and is rarely used directly in production
- Both Services rely on labels and selectors to find Pods

---

## Service Load Balancing (Observed Behavior)

### What was observed:
- Multiple Pods were running behind the same Service
- Traffic sent to the Service was distributed across Pods
- When a Pod was deleted, a new Pod was created automatically
- The Service continued working without any change to the client

### Key insight:
Clients always talk to Services, not Pods. Kubernetes handles Pod changes transparently.

---

## Role of Labels and Selectors

### Definition:
Labels are key-value pairs attached to Kubernetes objects, and selectors are used to match them.

### DevOps meaning:
Labels are the backbone of Kubernetes networking. Services and controllers rely on labels to manage and route traffic.

### Why it exists:
Labels provide a flexible and scalable way to group and manage resources dynamically.

---

## Kubernetes Commands Used (Day 3)
```bash
kubectl get pods
kubectl get pods -o wide
kubectl get svc
kubectl describe svc
kubectl get endpoints
kubectl scale deployment
kubectl delete pod
```

---

## Key Takeaways (Day 3)

- Services provide stable networking for dynamic Pods
- ClusterIP is used for internal communication
- NodePort is mainly for learning and testing
- Services use labels and Endpoints to route traffic
- Kubernetes networking remains stable even when Pods change

