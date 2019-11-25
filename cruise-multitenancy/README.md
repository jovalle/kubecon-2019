# Kubernetes at Cruise: Two Years of Multitenancy

| [Event](https://sched.co/UaaO) | [Presentation](presentation/Kubernetes%20Multitenancy%20-%20Karl%20Isenberg%20-%20KubeCon%20NA%202019.pdf) |
| - | - |

**Speakers**
* Karl Isenberg, Cruise

**Notes**
* TIL about Cruise, an autonomous vehicle development company
* backed by GKE and:
  * Nginx
  * Spinnaker
  * Stackdriver + Datadog
  * Hashicorp Vault
* Running ~1000 nodes in largest cluster (n1-standard-{32,64}!)
* Nine layers of isolation in multitenancy (sorted in descending isolation/cost)
  * System
  * Integration
    * Private ingress via interconnect (AWS, on-prem...)
  * Network
    * CNI bandwidth plugin (Calico)
    * Istio rate limits (quota rules)
    * Calico network policies
    * Istio service authorization, rule based access
  * Resource
    * Built-in types
    * Storage volumes
    * Quotas and limits
  * Permission
  * Domain
  * Identity
* Internal app called k-rail for policy enforcement
  * prohibits bind mounts, host network/PID, privileged containers, helm use, etc.
  * not OSS
* Using internal CRD for syncing RBAC across clusters