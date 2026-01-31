# Day 3 – Kubernetes Services

## What is a Service?

### Definition:
A Service is a Kubernetes resource that provides a stable network endpoint to access Pods.

### DevOps meaning:
Services allow applications to be accessed reliably even when Pods are recreated, scaled, or replaced.

### Why it exists:
Pod IPs are temporary and cannot be exposed directly. Services solve this by using labels and stable networking.

---

## NodePort Service (Hands-On)

- NodePort exposes an application on a fixed port of the node
- Traffic flows from the node to the Service and then to Pods
- Used mainly for local testing and learning

---

## Observations

- Pod IPs can change, but Service access remains stable
- Services use labels to discover Pods
- Kubernetes automatically load-balances traffic across Pods

---

## ClusterIP vs NodePort

### ClusterIP
- Default and most commonly used Service type
- Exposes applications only inside the cluster
- Used for internal communication between services
- Provides better security by default

### NodePort
- Exposes applications on a port of each node
- Used mainly for learning and local testing
- Not commonly used directly in production

---

## Service Load Balancing (Observed)

- Services route traffic using Endpoints
- Endpoints represent the current list of healthy Pods
- When Pods are deleted or recreated, Endpoints update automatically
- Clients are not affected by Pod changes

