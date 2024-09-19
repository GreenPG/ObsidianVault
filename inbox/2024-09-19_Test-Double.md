---
date: 2024-09-19
tags:
    - Doc
hubs:
    - "[[Testing]]"
urls:
    - http://xunitpatterns.com/Test%20Double.html
---


# Test Double 

Sometimes the test of the *system under test* (**SUT**) is made more complicated because it depends on other components. We can replace this dependences by a *Test Double*.
It merely have to provide the same API as the real *depended-on component* (**DOC**)

## How it works
During the **fixture setup** phase of the test, replace the DOC with the *Test Double*. Depending of the kind of tests, the behavior of the **TD** may be hard-coded or configured during the setup phase. 

It must be keeped in mind that you don't need to implement the whole interface of the DOC. Only the funcitonnality needed for the particular test. 

## When to use it

There are several circumstancs in wich it might be useful to use some sort of **TD** during tests:
- if there are *Untested Requirement* tat cannot be verified because neiteher the SUT or the DOC provide an observation point for the SUT' indirect output that is needed to be verified.
- if there are *Untested Code* and DOC does not provide the control point to allow us to exercise the SUT with the necessary indirect inputs
- if there are *Slow Tests* and we want to be able to run the tests more quicky and hence more often

Care must be taken when using **TD** because the SUT is tested in a different configuration from that which be used in production. So there must be at least one test that verifies that it works without a **TD**.
Care must also be taken to not replace the parts of the SUT that are to be tested. Also, excessive use of **TD** can results in *Fragile Tests* 

**TD** exists in different variations classifed based on how/why the **TD** is used:
- **Test Stub**:
    To replace a real component on whic the SUT depends so that the test has a control point for the indirect inputs of the SUT. Allow the test to force the SUT down paths it otherwise not execute.






*indirect input*:when the behavior of the SUT is affected by the values returned by another component whose services it uses.
