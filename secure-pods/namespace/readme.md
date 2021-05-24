### Secure namespace through OPA gatekeeper

Namespaces are high level objects within kubernetes cluster as they are available globally clusterwide. To create any k8s object one must have namespace and these namespaces are isolated and allows the user with multi-tenancy capabilities. Therefore, it is necessary to secure the namespace with security policies. 

Apply the template and constriants with the below commands
```
kubectl apply -f ns-secure-template.yaml
kubectl apply -f ns-secure-constraints.yaml
```
- This template allows any user on the k8s cluster to create namespace with the label tag. This allows transperancy during the audit purpose about who owned/owns the namespace.
1. Namespace should to be create with label 'owner'