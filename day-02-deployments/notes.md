## Why Deployments are used in production

- Deployments use controllers to enforce dersired state
- ReplicaSets ensure the correct number of Pods are always running
- If a Pod is deleted or crashes, it is recreated automatically
- This provides self-healing and high availability

