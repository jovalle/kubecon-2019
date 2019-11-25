# Solving Multi-Cluster Network Connectivity with Submariner

| [Event](https://sched.co/UadI) | [Presentation](presentation/Submariner%20Kubecon%20NA%202019.pdf)
| - | - |

**Speakers**
* Chris Kim, Rancher Labs
* Miguel Angel Ajo, Red Hat

**Notes**
* Kubernetes cluster networking model limited to network contained within a cluster
* Cloud providers enable connecting VPCs together but only within the confines of the particular cloud provider
* first prototype was just a bash script that createed IPsec tunnels using StrongSwan
* now capable of IPsec via CRDs
* does not support
  * overlapping IP CIDRs
  * DNS service discovery across clusters
  * netpols across clusters
  * many network plugins
* [lighthouse](https://submariner.io/lighthouse), solution to multi-cluster DNS discovery
* [coastguard](https://submariner.io/coastguard), solution to multi-cluster network policy