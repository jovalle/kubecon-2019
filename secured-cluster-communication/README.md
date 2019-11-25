# How Kubernetes Components Communicate Securely in Your Cluster

| [Event](https://sched.co/UaZE) | [Presentation](presentation/KubeCon%20NA%202019%20-%20How%20Kubernetes%20components%20communicate%20securely%20in%20your%20cluster%20-%2020191121.pdf)
| - | - |

**Speakers**
* Maya Kaczorowski, Google

**Notes**
* everything needs a certificate (use kubeadm to generate and import certs yourself)
* components get certs via certificates.k8s.io
  * activate with:
    * ```--cluster-signing-cert-file```
    * ```--cluster-signing-key-file```
  * CSR process:
    1. create request
    2. send request to apiserver
    3. approve request
    4. download and use cert
* check certs (stable in 1.15): ```kubeadm alpha certs check-expiration
* renew certs: 
  * automatically (stable in 1.15, default in 1.17 for node): ```kubeadm upgrade apply --certificate-renewal=true```
  * manually: ```kubeadm alpha certs renew``` (--use-api)
* rotate certs (beta in 1.8):
  * kubelet: ```--rotate-certificates```
  * kube-controller-manager: ```--experimental-cluster-signing-duration```
1. from the apiserver to the kubelet
  * from the apiserver to the kubelet
    * ```--kubelet-certificate-authority``` to specify CA to verify kubelet's server certificate
  * from the apiserver to node, pod, or service
    * plain http so it should never happen
2. from the kubelet to the apiserver
  * from the kubelet to the apiserver
    * requests over TLS (mTLS in ```Node Authorizer``` mode)
    * apiserver listens on HTTPS port 443
    * in ```Node Authorizer``` auth mode, kubelets use a credential in the system:nodes group
  * from the pod to the apiserver
    * server-only auth TLS
    * client authenticates with bearer token
3. between apiserver and etcd
  * from apiserver to etcd
    * localhost:80, mTLS with ```--etcd-certfile``` and ```--etcd-keyfile```
  * from etcd to apiserver
    * port 443
4. etcd to etcd
  * mTLS
5. admin to apiserver
  * options include:
    * OAuth tokens
    * x509 client certs
    * basic auth
    * auth proxy
    * anon auth (**DO NOT ALLOW!!!**)
6. other connections
  * from node to node
    * dependent on infra
  * from pod to pod
    * unauthenticated and not encrypted
    * use netpols to restrict and service mesh to encrypt traffic
  * all other connectivity should be dropped or disallowed