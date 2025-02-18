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

1.  High Availability
It's vital to select a technology robust enough to service trafic reliably to:
- Users (SSH keys, account password). They expect to be provisioned with credentials
rapidly in case of accident. 
- Applications (database credentials and API keys). Non performant service could degrade
  the availabilty of dependent applications or increase startup times

2. Centralize and Standardize

Secrets might be consumed differently over teams of a same company. It is then necessary
to to standardize and centralize the secrets management solution. Even when secrets
management is centralized, you may use secondary secrets management to secure the
primary. Standardization then ensure maintainability and usability.
Standardization should include secrets life cycle management, authentication,
authorization and accounting of the secrets management solution.

3. Access control

Least Privilege principle should be applied to avoid leak. The secret management
system must provides the ability to configure fine granular access controls on each
object and component to accomplish the [Least Privilege principle](obsidian://open?vault=ObsidianVault&file=inbox%2F2025-02-18_Least_Privilege_principle).


4. Automate Secrets Management

Manual maintenance increase the risk of leakage and human errors. It can also become
wasteful. It's better to limit or remove the human interaction with the actual secrets.
You can restrict in in multiple ways:
- 
