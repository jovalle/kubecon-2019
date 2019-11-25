# Kubernetes Policy Enforcement Using OPA at Goldman Sachs

| [Event](https://sched.co/UaaX) | [Presentation](presentation/OPA-kubecon-final.pptx)
| - | - |

**Speakers**
* Tim Hinrichs, Styra
* Miguel Uzcategui, Goldman Sachs

**Notes**
* Goldman Sachs has a tiny k8s portfolio (only 18 cluster total!)
* They use Ceph/Rook X_X
* Policy set disallowing the use of both ingress controllers for same target host:
```
package kubernetes.admission
import data.kubernetes.ingresses
deny[msg] {
    input.request.kind.kind == "Ingress"
    newhost := input.request.object.spec.rules[_].host
    oldhost := data.kubernetes.ingresses[namespace][name].spec.rules[_].host
    newhost == oldhost
    msg := sprintf("host conflicts with ingress %v/%v", [namespace, name])
}
```
* Gitlab repo as source of truth for policies, Gitlab CI/CD for propogating changes to all clusters
* OPA metrics:
  * Go routine and thread counts
  * Memory in use (stack vs heap)
  * Memory allocated (stack vs heap)
  * GC stats
  * Pointer lookup count
  * Roundtrip time by http method
  * GCC time
  * Percentage of requests under 500ms, 200ms, 50ms
  * Mean API request latency
  * Number of OPA instances up at any given time
  * OPA responding under 200ms for 95% of requests
* OPA bundles > OPA API push
* Create metrics dashboard before production
* never use static data, use version control, use CI/CD pipelines to rollout/rollback changes