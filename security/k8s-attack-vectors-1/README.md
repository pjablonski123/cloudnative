## Kubernetes attack vectors

Typically a real scenario attack is based on an exploit composition of multiple threat vectors. It can start from a Layer 7 threat vector inflicted by a well-known log4shell vulnerability. But this is not enough to take control over the underneath Kubernetes cluster. There are other contributors. There may not be good enough isolation which allows lateral movement. Then a threat actor can jump to a less strict environment where an RBAC policy grants permissions to create pods for devops.

In the attached presentation we provided together Fulya Sengil you can find such an attack scenario with commands exploiting threat vectors.

A few comments:
1. The scenario starts from the rootless non-privileged ready-only deployment and ends up with its own standalone container. Choose a solution which can monitor and protect not only K8s but also the host and standalone containers beyond any orchestrator.
2. To set up a reverse shell a threat actor does not need ncat. They can just use the tcp connect with bash command. Harden your images and make them immutable providing changes through a structured CICD process with security scanners onboard.
3. Avoid pods with hostPID, hostIPC and privileged mode set to true. Privileged settings may be used by debug pods. Use them wisely with monitoring and limitations or don't use them at all.
4. Use solutions which can block by default commands like nsenter. The attacker can attach itself to a host's namespace and a filesystem and execute commands like a host.

A slide deck:
[Prisma Cloud webinar_ Kubernetes Threat Vectors and Prevention.pdf](https://github.com/pjablonski123/cloudnative/files/10948398/Prisma.Cloud.webinar_.Kubernetes.Threat.Vectors.and.Prevention.pdf)

A session recording: 
https://register.paloaltonetworks.com/kubernetesthreatvectorsandpreventionkubernetesthre
https://event.on24.com/wcc/r/4090089/2BA80AB024B9AF729402515C037EDE78
