---
date: 2025-02-18
tags:
    - #Doc 
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
object and component to accomplish the [Least Privilege principle](obsidian://open?vault=ObsidianVault&file=inbox%2F2025-02-18_Least_Privilege_principle).


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
managemnent system and tested routinely.

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



