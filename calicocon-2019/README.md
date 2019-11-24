# CalicoCon

| [Event](https://sched.co/Uk9r) | [Presentation](presentation/CalicoCon\ 2019.pdf) | [Exercises](https://github.com/jovalle/calicocon-2019) | [Product Page](https://projectcalico.org) |
| - | - | - | - |

**Speakers**
* Jonathan Sabo, Tigera
* Karthik Prabhakar, Tigera
* Brandon Josza, Tigera

**Notes**
* Default CNI solution on all managed Kubernetes services today!
* XDP/eBPF supported since Calico 3.8
* With IPVS we can scalled to 10K services with half the bottleneck compared to iptables (overally small detriment compared to say 1K services)
* Host endpoint protection on etcd/jumphosts = profit!
* External IP Pools? If we can find the IPs
* ```GlobalNetworkPolicy``` can be applied to specific namespaces via ```namespaceSelector``` (or just continue using Calico ```NetworkPolicy```)