## Why pods are not used directly in production

- Pods do not self-heal
- If a Pod is deleted or crashes, it does not come back
- kubernetes only recreates pods when a controller (like deployment) exists
- Devops teams use deployment to ensure availability
