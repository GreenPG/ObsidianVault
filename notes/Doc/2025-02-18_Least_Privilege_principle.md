---
date: 2025-02-18
tags:
    - #Doc
hubs:
    - "[[DevOps]]"
urls:
    - https://en.wikipedia.org/wiki/Principle_of_least_privilege
---

# Least Privilege principle 

The Least Privilege principle require that in a particular abstration layer of a
computing environment, eveery module must be able to access only the information and
ressources that are necessary for its legitimate purpose.

## Details

It means giving any user accounts or processes only those privileges which are
essentially vital to perform its indended functions.

The principle is widely recognized as an important design consideration towards
enhancing and giving a much neede boost to protection of data and functionality from
faults and malicious behavior.

Benefits of the principle:
- **Intelectual Security**: it's eaiser to test code possible actions and interaction
whit other security targeted applications when its scopes is limited.
- **Better system security**: when code is limited in the system-wide actions it may
perform, vulnerabilites in one application can't be used to exploit the rest of the
machine.
- **Ease of deployment**: the fewer privleges an application requires, the easier it is
  to deploy within a larger environment. This usually results from the first two
benefits, applications that install device drives or require elevated security
privileges typically have additional steps int their deployment.

