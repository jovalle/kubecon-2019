# Use Your Favorite Developer Tools in Kubernetes with Telepresence

| [Event](https://sched.co/UaeA) | [Presentation](presentation/Use%20Your%20Favorite%20Developer%20Tools%20With%20Telepresence.pdf)
| - | - |

**Speakers**
* Abhay Saxena, Datawire

**Notes**
* debugging a service can be difficult. telepresence allows you to bring a service to your local environment by relaying connectivity to your local instance
* use Debugger in an IDE to deploy a local instance
* ```telepresence -s <DEPLOYMENT> --to-pod=<PORT> --docker-run --rm -it <IMAGE>```
* BUT: doing so can cause outages as you debug so use something like Datawire's Edge gateway for simultaneous connectivity between local and remote (use HTTP headers to specify destination)