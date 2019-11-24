# Tutorial: A Kind Workflow for Contributing to Kubernetes

| [Event](https://sched.co/Uaek) | [Presentation](https://hackmd.io/@mauilion/kind-workflow/)
| - | - | - |

**Speakers**
* James Munnelly, Jetstack
* Benjamin Elder, Google
* Patrick Lang, Microsoft
* Duffie Cooley, VMware

**Notes**
* Recommended for e2e testing by top Kubernetes contributors from all corners of the industry
* Run anywhere with docker
* k8s.work for demoing working parts of KinD deployment process, ideally just ```brew install kind```
* Benjamin Elder, writer of most of KIND, is a sweetheart. Sold me on KIND. Highly advises disposable VMs instead of nested KIND (i.e. docker container) for greater stability and performance. Nested KIND is obviously supported (and "stable") but only due to demands not by desire.
* On mac, kubectl proxy + metallb (L2 mode)