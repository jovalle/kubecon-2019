# Securing Your Services with Authentication, Authorization, and RBAC in gRPC

| [Event](https://sched.co/Uad3) | [Presentation](presentation/luis-pabon-securing-your-gRPC-service.pdf)
| - | - |

**Speakers**
* Luis Pabón, Portworx

**Notes**
* authentication:
  * who are you?
  * how can I trust that you are who you say you are?
  * what other information is there about you?
* authorization:
  * are you allowed to do what you are asking?
  * are you allowed to access that information?
* no password management!!!
* use JWT (JSON Web Token) to identify a user
  * ```[ header . claims . signature ]```
    * header: token and signature types in clear text
    * claims: JSON formatted metadata about the user in clear text
    * signature: created using crypto hash
* gRPC apps should only verify the token from trusted issuer
* [golang token example](https://github.com/libopenstorage/openstorage-sdk-auth/blob/892edc04561b26f6531fdda4383b2e0da55cc789/pkg/auth/auth.go#L57-L70)
