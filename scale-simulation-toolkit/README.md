# A Toolkit for Simulating Kubernetes Scheduling at Scale

| [Event](https://sched.co/UaVk) | [Presentation](presentation/JD-JoySim.pdf)
| - | - |

**Speakers**
* Yuan Chen, JD.com

**Notes**
* China's largest retailer
* Why a simulator?
  * evaluating new configs and features before deploying to prod
  * control plane performance and scalability benchmarks and optimization
  * time consuming and costly to perform such evaluations at scale
  * simulate large-scale k8s clusters with a small amount of resources
* MockNode is a simulated kubelet
* a MockServer can simulate 100+ MockNodes while only conusming 8CPU and 16GB RAM
* “1800 simulation containers, 6 MockNodes (60 CPU cores, 300GB) per container. Simulate 11,400 nodes, 200,000+ containers“
* no demo :(