# Understanding and Troubleshooting the eBPF Datapath in Cillium

| [Event](https://sched.co/Uae7) | [Presentation](presentation/eBPF%20and%20the%20Cilium%20Datapath.pdf)
| - | - |

**Speakers**
* Nathan Sweet, DigitalOcean

**Notes**
* "the network is the bottleneck"
* "a CNI and replacement for kube-proxy"
* Cillium appends a number of features to layers 2/3/4
  * determines what to do with packets at NIC level (L2, XDP)
  * provides Network Policy CRD (cgroups, netfilter, xfm4_policy), Services (ip_routing, netfilter, sock_ops) with eBPF