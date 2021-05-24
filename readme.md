# Open Policy Agent - OPA
OPA provides flexibily to enforce RBAC on your kubernetes cluster effeciently. Policies are declared using Rego language. For more details check <a href="https://www.openpolicyagent.org/"> here</a>

### Pre-requisites
* Kubernetes cluster (Managed or bare metal) Version 1.14 above
* Atleast one worker node Version 1.14 above
* Helm package manager Version.3


### Helm installation
```
helm repo add gatekeeper https://open-policy-agent.github.io/gatekeeper/charts --force-update
helm install opa --create-namespace -n gatekeeper-system --wait gatekeeper/gatekeeper
kubectl apply -f config.yaml
```

### Manual installation
```
kubectl apply -f https://raw.githubusercontent.com/open-policy-agent/gatekeeper/release-3.1/deploy/gatekeeper.yaml

```

## How to use?

- Each directory contains 3 files 
1. Template
2. Constraint
3. Violation

- For ready to use in production refer <b><a href="https://github.com/ashokjjk/gatekeeper-k8s-library/tree/master/secure-pods">secure-pods</b></a> directory which contains all the major security policies that are baked together into a single template, constraint under 3 directories with sample violation and non-violation manifest.



### Uninstall Helm
```
helm uninstall opa
```
- Uninstalling helm package will not totally clear the gatekeeper from the cluster as it leaves some crd footprints. To do deep clean use the manual procedure below after unistalling helm. 


### Deep clean OPA gatekeeper
<p>If you do not use Helm package manager then proceed with below procedure to destroy everything that was created by OPA Gatekeeper.</p>

```
kubectl delete ns/gatekeeper-system
kubectl delete constrainttemplates --all
kubectl delete crd/configs.config.gatekeeper.sh
kubectl delete crd/constraintpodstatuses.status.gatekeeper.sh
kubectl delete crd/constrainttemplatepodstatuses.status.gatekeeper.sh
kubectl delete crd/constrainttemplates.templates.gatekeeper.sh
kubectl delete podsecuritypolicy gatekeeper-admin
kubectl delete clusterrole gatekeeper-manager-role
kubectl delete clusterrolebinding gatekeeper-manager-rolebinding
kubectl delete validatingwebhookconfiguration gatekeeper-validating-webhook-configuration
```

### References
1. https://github.com/open-policy-agent/gatekeeper
2. https://github.com/open-policy-agent/gatekeeper-library
3. https://www.magalix.com/blog/introducing-policy-as-code-the-open-policy-agent-opa
4. https://www.magalix.com/blog/integrating-open-policy-agent-opa-with-kubernetes-a-deep-dive-tutorial
5. https://katacoda.com/austinheiman/scenarios/open-policy-agent-gatekeeper
6. https://www.katacoda.com/cloudsecops/courses/opagatekeeper-policy
7. https://play.openpolicyagent.org/p/8SowEXjNqk
