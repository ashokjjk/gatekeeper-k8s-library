### General OPA gatekeeper security policies

<p>Gatekeeper uses a template to apply the RBAC polices through under the hood k8s objects called as Pod Security Policies (PSP). However comparing PSP with Gatekeeper provides greater leverage and flexibility for anyone to enforce policy as a code on each objects to micro level.</p>

- This directory contains <b> gen-template.yaml</b> file which holds the general security policies written using Rego language templates. This template contains the below actions

1. Pull container images only from secure repo
2. Use only secure directory paths on node 
3. Pod manifest should only use allowed imagePullPolicy
4. All pods should have readiness/liveness probes along with probe types
5. Restrict a pod with image tags specifications. eg. nginx:latest
6. All pods should have limits specified and it should be lower than the constraints
7. No container should run in privileged mode for both init and general containers
8. No pod manifest should have hostPID, hostIPC declared as true

- <b> gen-constriants.yaml</b> file which holds the constraints that should be enforced to the template.

*** It is manadatory that before going any further to use this template and constraints on the cluster, OPA gatekeeper must be installed inside the cluster and config.yaml to be added to the cluster to provide general configurations.

Just like applying all other kuberentes object use the below command to apply the template
```
kubectl apply -f ../config.yaml
kubectl apply -f gen-template.yaml
kubectl apply -f gen-constraints.yaml
``` 
- Please check the behaviour of gatekeeper by introducing a violated pod through the given k8s manifest <a href="https://raw.githubusercontent.com/Sage/it-sage-commerce-infrastructure-sandbox/opa/violation.yaml?token=ARJTYQAO3TXO6J3RKYB5TT3AV5OOG">here</a>.
- Check gen-constraints.yaml for allowed registry, host paths, probes, policies, tags, resource limits
- To exclude a namespace from the above policy enforcement, it can be done by specifying it on the constraint if not this policy will be applied globally across the cluster.
- To add more leverage we also have config.yaml where we can specify excludeNamespace from certain gatekeeper actions