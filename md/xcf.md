## Integrating the Healthcare Enterprise
![IHE](../img/ihe.png)
# IHE IT Infrastructure<br/>Technical Framework Supplement<br/><br/>Cross-Community Fetch (XCF)<br/><br/>Rev. 1.5 – Trial Implementation

### Date: July 21, 2017<br/>Author: ITI Technical Committee<br/>Email: iti@ihe.net

#### *Please verify you have the most recent version of this document. See here for Trial Implementation and Final Text versions and here for Public Comment versions.*

#### *Copyright © 2016: IHE International, Inc.*

---

## Introduction
The Cross-Community Fetch (XCF) Profile defines a single transaction for accessing medical data between gateways that facilitate multiple dimensions of communication (trust, semantics, encoding, legislation, authority, etc.). The profile is highly inspired by the Cross Gateway Query/Cross Gateway Retrieve transactions and integrates these originally distinct transactions.

In specific use cases, for example when a few dynamically created documents need to be accessed from interacting communities with centralized data localization, a single transaction (versus independent query and retrieve) may reduce the coordination and maintenance of the transactional dependencies and transaction states.

For such use cases, and in environments where stateless Responding Gateways can be designed, it simplifies the implementation of such Responding Gateways. However, it may increase the implementation complexity of Initiating Gateways serving some types of communities, such as XDS Affinity Domains. XCF offers a different deployment option from the general purpose XCA Profile.

## Open Issues and Questions
**XCF008**: This supplement introduces the concept of automated document transforms at the XCF Responding Gateway while not necessarily making the transformed document persistent. For patient safety and traceability reasons this aspect might need to be discussed further.

**XCF009**: The relationship/difference to on-demand should be provided.

