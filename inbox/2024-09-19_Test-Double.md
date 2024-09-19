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
- **Test Spy**:
    A more capable version of Test Stub. It has an observation point for the indirect outputs of the SUT. Like Test Stub, it needs to provide values to SUT in response to method calls but also captures the indirect outputs of the SUT and saves them for later verification.
- **Mock Object**:
    Used as observation point used to verify the indirect outputs of the SUT. It also includes the functionnality of the Test Stub (must return values to the SUT) the emphasis is on the verification of the indirect outputs. It's much more than just a Test Stub with assertion, it's used in a fundamentally different way.
- **Fake Object**:
    Replace the funcitonnality of a real DOC for other reasons that verification on indirect inputs of the SUT. It implements the same funcitonnality as the real DOC but in a much simplet way. It is build specifically for testing, but is not used either as control point or an observable point.
    The most common reason to use it, is that the real DOC is not avalaible yet, too slow or cannot be used in the test environement because of deleterious side effects.
- **Dummy Object**:
    Some method of the SUT may requires objects as parameters that neither the SUT, nor the test care about. In this case, you may pass a Dummy Object wich maybe a as simple as a null object reference, an instance of the Object class or an instance of a Pseud Object.




*indirect input*:when the behavior of the SUT is affected by the values returned by another component whose services it uses.
