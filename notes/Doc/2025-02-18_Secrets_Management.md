---
date: 2025-02-18
tags:
  - Doc
hubs:
  - "[[DevOps]]"
urls:
  - https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html
---

# Secrets Management

## General Secrets Management

### 1.  High Availability
It's vital to select a technology robust enough to service trafic reliably to:
- Users (SSH keys, account password). They expect to be provisioned with credentials
rapidly in case of accident. 
- Applications (database credentials and API keys). Non performant service could degrade
  the availabilty of dependent applications or increase startup times

### 2. Centralize and Standardize

Secrets might be consumed differently over teams of a same company. It is then necessary
to to standardize and centralize the secrets management solution. Even when secrets
management is centralized, you may use secondary secrets management to secure the
primary. Standardization then ensure maintainability and usability.
Standardization should include secrets life cycle management, authentication,
authorization and accounting of the secrets management solution.

### 3. Access control

Least Privilege principle should be applied to avoid leak. The secret management
system must provides the ability to configure fine granular access controls on each
object and component to accomplish the [[2025-02-18_Least_Privilege_principle|Least Privilege]].


### 4. Automate Secrets Management

Manual maintenance increase the risk of leakage and human errors. It can also become
wasteful. It's better to limit or remove the human interaction with the actual secrets.
You can restrict in in multiple ways:
- **Secrets pipeline**: having a secret pipeline which does large parts of the secret
management
- **Using dynamic secrets**: they should be used where possible to reduce the surface
area of credential reuse.
- **Automated rotation of static secrets**: key rotation is a challenging process when
implemented manually. It's therefore better to automate the rotation of keys or at least
ensure that the process is sufficiently support by IT.

### 5. Handling Secrets in Memory

Additional level of security can be achieved by minimizing the time window where a
secret is in memory and limiting the access to its memory space, even it's could be a
difficult implementation.
It can be easy with lower languages but much more difficult with higher level language
with garbage collector.

### 6. Auditing

It's an essential parts of secrets management. It must be implemented securely to be
resilient against attempt to tamper with or delete the audit logs. At minimum, you
should audit:
- who request a secret and for whant system and role
- wheter the request was approved or not
- when the secrets was used and by whom/what
- when it expired
- whether there were any attempts to re-use expired secrets
- if there have been any authentication or authorization errors
- when the secret was updated and by whom/what
- any administrative actions and possible user activity on the underlying supporting
infrastructure stack.

All auditing must have a timestamps.

### 7. Secret Lifecycle

Secrets follow a lifecycle. Thes stages are as follows:
- Creation
- Rotation
- Revocation
- Expiration

1. **Creation**

New secrets must be securely generated and cryptographically robust enough for their
purpose. They must have the minimum privileges assigned to them to enable their
required use/role.
Credentials should be transmit securely, i.e. password and username should not be sent
along when requesting user accounts. 


2. **Rotation**

Secrets should be regularly rotated so that any stolen credentials will only work for a
short time. It will also reduce the tendency for users to fall back to bad habits.

User credentials are excluded from regular rotating, except if there is a suspicion or
evidence that they have been compromised.


3. **Revocation**

When secrest are no longer required or potentially compromised, you must securely
revoken them to restrict access. Whith (TLS) certificates, this also involves certifacte
revocation

4. **Expiration**

Secrets should expire at a defined time where possible. It can be activate by the secret
consuming system, or an expiration date set at the secrets management system forcing
supporting processes to be triggered, resulting in a secret rotation.
App should verify that the secrets is still active before trusting it.

### 8. Transport Security Layer (TLS) Everywhere

Never transmits secrets via plaintext.

### 9. Downtime, Break-glass, Backup and Restore

Maintenance windows must be carefully chosen based on earlier metrics and audit logs.

Backup and restore procedure of the system should be regularly tested and audited for
their security. Ensure that:
    - an automated backup procedure is in place and executed periodaically. Base the
      frequency of the backups and snapshots on the number of secrets and their
      lifestyle
    - frequently test restore procedures to guarantee that the backups are intact
    - encrypt backups and put them on secure storage with reduced access rights. Monitor
      the backup location for access and administrative actions.

Emergency process ("break-glass") should be implemented to restore the service if the
system becomes unavailable for reasons other than regular maitenance. Emergency
break-glass credentials should be regularly backed-up securely in a secondary secrets
management system and tested routinely.

### 10. Policies

Consistently enforce policies defining the minimum complexity requirements of passwords
and approved encryption at an organization-wide level. Using centralized secrest
management solution can ehlp/
Having organization-wide secrets management policy can help enforce applying the best
practicies.

### 11. Metadata: prepare to move the secret

A secret management solution should provide the capability to store a least the
following metadata about a secret:
- when it was created/consumed/archived/rotated/deleted
- who created/consumed/archived/rotated/deleted it
- what created/consumed/archived/rotated/deleted it
- who to contact when having problem with the secret or having questions about it
- for what the secret is used
- what type of secret it is
- when you need to rotate it, if done manually


## CI and CD

CI/CD tools store secrets to provide configuration to application during deployment, and
alternatively interact heavily with the secrets management system. Various best
practices can help smooth secret management in CI/CD.

### Hardening your CI/CD

- Treat your CI/CD tooling as a production environment: hardent it, patch it and harder
  the underlying infrastructure and services
- Have security event monitoring in place
- Implement least-privilege access: developers do not need to be able to administer
projects. They only need to be able to execute required functions (setting up pipleines,
running them). There is no need for privileged roles that might have access to secrets
- Make sure tath pipeline output does not leak secrets, and you can't listen in on
production pipelines with debugging tools
- make sure you cannot exec into any runners and workers for a CI/CD system
- have proper authentication, authorization and accounting in place.
- Ensure only an approved process can create pipelines

### Where a secret should be ?

There are various places where you can store secrets to execute CI/CD actions:
- as port a the CI/CD
- as port of the secrets management system. The CI/CD pipeline would require credentials
  to connect to these secrets management system, to have secrets in place.
- use the CI/CD pipeline to leverage the encryption as  a service from the secrets
management system to do the encryption of a secret and commit it to git. The consuming
service can then fetch it on deployment and decrypt it.

### Authentication and authorization of CI/CD tooling

CI/CD should have designated service accounts, which can only operate in the scope of
the required secrets of orchestration of the consumers of a secret. Additioally, a CI/CD
pipeline run should be easily attributable to the one who has defined the job or
triggered it to detect who has tried to exfiltrate secrets or manipulate them.

### Logging and accounting

Every action in a CI/CD tool should be logged. You should define security alerting rules
at every non-standard manipulation of the pipeline tool and its administrative interface
to monitor secret usage.

### Rotation vs Dynamic creation

CI/CD tooling can be used to rotate secrets or instruct other components to do the
rotation of the secret.
Alternatively, the CI/CD or another component could setup a dynamic secret: a secret
required for a consumer to use for as long as it lives. It is invalidated when the
consumer no longer lives.

### Pipeline created secrets

Pipeline tooling can be used to generate secrets and either offer them directly to the
service deployed by the tooling or provide the secret to a secrets management solution.
Alternatively, the secret can be stored encrypted in git so that the secret and its
metadata is as close to the developer's daily place of work as possible.
It requires that the devs can't decrypt the secrest themselves and that every consumer
of a secret has its encrypted variant of the secret.

## Containers and Orchestrators

### Injection of secrets

There are three ways to get secrets to an app inside a docker container:
- **Mounted volumes**: secrets are kepts within a particular config/secret file mounted
  to the instance as a mounted volume. Ensure that these files are mounted by the
orchestrator and never built-in. Make sure that the orchestrator mounts in the volume
when required
- **Fetch from the secret store**: a sidecar app/container fetches the secrets it needs
  directly from a secret manager service without dealing with docker config.
- **Environment variables**: secrets can be provide directly as port of the docker
container configuration. They should never be hardcoded using docker ENV or  ARG
command. Additioally, environment variables are generally accessible to all processes
and may be included in logs or system dumps. Using environment variables is therefore
not recommended unless the other mtehods are not possible

### Short lived side-car containers

You can create short-lived sidecar container that fetch secrets from some remote
endpoint and then store them on a shared volume mounted to the original conatiner which
can now use them from the mounted volume.
This way, there's no need to integrate third-party tool or code to get secrets. 
Once the sidecar has fetched the secrest, it terminates.

### Internal vs External access

You should only expose secrets to communication mechanisms between the container and the
deployment representation. Never expose secrets through external accesss mechanisms
shared among deployments or orchestrator.
When the orchestrator store secrets, make sure that the stoarage backend of the
orchestrator is encrypted and you manage the keys well.

## Implementation guidance

### Dynamic vs Static use cases

Use cases for dynamic secrets:
- short-lived secrets (credentials or API keys) for a secondary service that expresses
the intent for connecting the primary service to the service
- short-lived integrity and encryption controls for guarding and securing in-memory and
  runtime communication processes. Encryption keys that only need to live for a single
session or a single deployment lifetime
- short-live credentials for building a stack during the deployment of a service for
interacting with the deployers and supporting infrastructure

Use cases for static secrets:
- long term secrets needed to create dynamic secrets
- key material that need to live longer than a single deployment with the service due to
  the nature of their usage in the interaction with other instances of the same service
- key material or credentials to connect to services that do not support creating
temporal roles or credentials

### Ensure limitations are in place

Secrets should never be retrievalbe by everyone and everything. Always make sure that
you put guardrails in place:
- Ensure that there are policies in place to limit the number of entities that can read
  or write the secret.
- Consider separating the production and development secrets by having separate secret
management solutions.

### Security event monitoring is key

Continually monitor who/what, from which IP, and what methodology accesses the secret.
There are various pattern where you need to look out for, such as:
- monitor who accesses the secret at the secret management system: is this normal
behavior ?
- monitor the service requiring the secret, whether the user of the secret is coming
from an expected IP, with an expected user agent.

### Usability

Ensure that your secret management solution is easy to use. It requires:
- easy onboarding of new secrets and removal of invalidated secrets
- easy integration with the existing software.
- a clear understanding of the organization of secrets management and its processes is
essential

## Encryption

### Encryption types to use

Various encryption types can be used to secure a secret as long as they provide
sufficient security, including adequate resistance against quantum computing-based
attacks.
It's best to take a look at sources like [keylength.com](https://www.keylength.com).

### Convergent encryption

Convergent encryption ensures that a given plaintext and its key results in the same
ciphertext. This can help detect possible re-use of secrets, resulting in the same
ciphertext. 
The challenge with enabling convergent encryption is that it allows attackers to use the
system to generate a set of cryptographic strings taht might end up in the same secret,
allowing the attacker to derive the plain text secret.

### Where to store the encryption keys ?

You should not store keys to the secrets they encrypt, except if those keys are
encrypted themselves.

### Encryption as a Service (EaaS)

Eaas is a model in which users subscribe to a cloud-based encryption service without
having to install encryption on their own systems. Using Eaas, you can get the following
benefits:
 - Encryption at rest
 - Encryption in transit (TLS)
 - Key handling and cryptographic implementations are taken care of by Encryption
 Service, not by developers
 - the provider could add more services to interact with the sensitive data

