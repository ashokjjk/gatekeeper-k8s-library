### Secure cluster from un-authorized container with OPA gatekeeper

The container inside a pod can use elevated privileges to run the root user and exploit the system by accessing any vulnerable packages from open network. It is necessary to restric such use inside the pod level so that no container can exploit the cluster or other containers inside the cluster.

Apply the template and constraint with the below commands
```
kubectl apply -f user-template.yaml
kubectl apply -f user-constraints.yaml
```
This template and constraint enforces the below actions
1. Restrict a pod to be created with the container that has root access
2. Pods can be created with the given user/group id ranges 
3. Check user-constraints.yaml file for allowed ranges