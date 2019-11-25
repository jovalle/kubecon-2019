# Running Istio and Kubernetes On-prem at Yahoo Scale

| [Event](https://sched.co/UaaO) | [Presentation](presentation/K8s\ \&\ Istio\ \@\ Yahoo.pdf) |
| - | - | - | - |

**Speakers**
* Suresh Visvanathan, Verizon
* Mrunmayi Dhume, Verizon

**Notes**
* using kubernetes since 2017
* 1000 apps, >1000 stateful, 2900+ nodes, 18 prod clusters, global
* Istio integration with mTLS everywhere
* custom ingress for extranet, envoy for intranet
* multiple sidecars: logging and metrics
* no clear picture behind their CI/CD which looks awfully generic (build -> deploy to k8s -> test). Not even a mention of post-test functionality/workflows.