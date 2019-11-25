# Multiple Networks for Kubernetes Workloads

| [Event](https://sched.co/UabS) | [Presentation]()
| - | - |

**Speakers**
* Doug Smith, Red Hat
* Piotr Skamruk, CodiLime

**Notes**
* flat networks need just one CNI but "what about for performance networking workloads?"
* CNI bridge plugin
  * bridge on host to pod via veth pair
* CNI multiplexer allows for selection of CNI (one interface on pod per attached CNI)
* CNI multiplexer is just a controller for a ```NetworkAttachment``` CRD, which details how a pod is to be attached to multiple networks
* Multus CNI supports ```NetworkAttachment```
* CNI-Genie allows for selecting CNI at deployment via annotations
```
...
kind: Pod
metadata:
  ...
  annotations:
    k8s.v1.cni.cncf.io/networks: flannel@eth1, customns/weavenet@eth2
    k8s.v1.cni.cncf.io/network-status: |-
      [
        ...
      ]
spec:
  ...
```
  * ```networks```: list of attachments to select
  * ```network-status```: detailed info of attachments
* Nokia DANM allows for more ESX-like expression but less flexible
```
...
kind: Deployment
...
spec:
  template:
    metadata:
      ...
      annotations:
        danm.k8s.io/interfaces: |
          [
            {"tenantNetwork":"management","ip":"dynamic"},
            {"clusterNetwork":"external","ip":"dynamic"},
            {"tenantNetwork":"internal","ip":"dynamic"}
          ]
spec:
...
```