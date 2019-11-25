# Liberating Kubernetes From Kube-proxy and Iptables

| [Event](https://sched.co/Uaam) | [Presentation](presentation/Liberating%20k8s%20from%20kube-proxy%20and%20iptables.pdf) | [Product Page](http://cilium.io) |
| - | - | - |

**Speakers**
* Martynas Pumputis, Cillium

**Notes**
* iptables has slow support
* iptable rule for each service and pod = too many
* Cillium packet flow (really XDP and (e)BPF) allows for dropping packets at host NIC level for relatively insane speeds and scaling potential
* no more kube-proxy! other talks have claimed that the greatest sources of cluster performance regressions at massive scale are ```DaemonSets``` and kubelets