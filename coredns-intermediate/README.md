# CoreDNS - Beyond the Basics

| [Event](https://sched.co/UaXI) | [Presentation](presentation/CoreDNS%20Beyond%20the%20Basics%20KubeCon%20NA%202019.pdf)
| - | - |

**Speakers**
* John Belamaric, Google
* Cricket Liu, Infoblox

**Notes**
* project started by Miek Gieben, author of Go DNS lib
* CoreDNS
  * written in go, memory-safe
  * built-in, k8s integration
  * plugin support
* DNSSEC (DNS Security Extensions)
  * digitally sign DNS zone data and support
    * origin auth
    * integrity checking
  * most top-level zones are signed (e.g. the root, com, net...)
  * most operators of recursive DNS services (e.g Google Public DNS, Cloudflare DNS, etc.) do DNSSEC validation
  * two forms of DNSSEC signing
    * on-the-fly via dnssec plugin
    * adding DNSSEC's resource reords to zone data file
* DNS over TLS (DoT)
  * CoreDNS can handle queries via tls:// prefix
    1. create TLS cert: 
      ```
      openssl req -new -newkey rsa:4096 -x509 -sha256 -days 365 -nodes-out MyCertificate.crt -keyout MyKey.key
      ```
    2. configure cert use
      ```
      tls://. {
        tls MyCertificate.crt MyKey.key
        forward . 8.8.8.8 8.8.4.4
        cache
      }
      ```
    3. validate cert chain
      ```
      echo | openssl s_client -connect '127.0.0.1:853' | grep -B 2 -A 5 "Certificatechain"
      ```
* manage zone data with git
  * [git-sync](https://github.com/kubernetes/git-sync)
  * ```docker run -d -v /etc/coredns:/tmp/git registry/git-sync \--repo=https://github.com/myzonedata --branch=master --wait=30```
* multicluster service discovery
  * [multicluster-dns](https://github.com/coredns/multicluster-dns) + [kubernetai](https://github.com/coredns/kubernetai)
  * each CoreDNS instance:
    * talks to every cluster APi server
    * serves up all local services
    * service up explicitly labeled remote services
  * service names
    * can be shared across clusters
    * can have unique cluster zones