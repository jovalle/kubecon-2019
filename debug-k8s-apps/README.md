# Tutorial: Debug Your Kubernetes Apps

| [Event](https://sched.co/UaeY) | [Presentation]() | [Repo](https://github.com/aws-samples/debug-k8s-apps)
| - | - | - |

**Speakers**
* Arun Gupta, Amazon
* Re Alvarez Parmar, Amazon

**Notes**
* Design considerations:
  * hosted or self-managed?
    * control plane
    * data plane
  * HA, DR (backup/restore etcd?)
  * availability zones?
* etcd uses the RAFT consensus protocol, RTFM
* troubleshooting checklist
  * check cluster configuration
  * networking
    * CNI
      * if pods (prematurely) halt scheduling, check available IPs via CNI's IPAM
      * try CNI Metrics Helper (aws/)
    * {kube,Core}DNS
      * check CoreDNS pod is running
      * enable logging in CoreDNS
      * check CoreDNS logs
      * scale up CoreDNS pods or convert CoreDNS to DS
      * memory required (MB) = (pods + services)/1000 + 54
      * worst case scenario: enable Autopath plugin (improved performance especially for external lookups but at much higher memory cost)
        * memory required (MB) = (pods + services)/250 + 54
    * kubectl
      * don't use env vars in kubeconfig to avoid spidering
    * monitoring
      * enable readiness/liveness probes across ALL containers (no exceptions)
      * tracing (OpenTracing)
      * capture process health/metrics/logs
    * resources
      * avoid oversusbcription using resource limits and requests
      * set resource quotas per namespaces
        * once quota reached, future pods will fail to schedule ("forbidden...exceeded quota...")
      * use LimitRange to set default limit
* commands
  * show Pending pods
    * ```kubectl get pods --field-selector involvedObject.kind=Pod.type=Pending```
  * check API is accessible
    * ```curl -k http://CLUSTER_ENDPOINT/api/v1```
  * show resource usage
    * kubectl top nodes