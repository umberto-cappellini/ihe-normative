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

---

# Volume 1 – Profile

## 29 Cross-Community Fetch (XCF) Profile
The Cross-Community Fetch (XCF) Profile defines a single transaction for accessing medical data between gateways that facilitate multiple dimensions of communication (trust, semantics, encoding, legislation, authority, etc.). The profile is highly inspired by the Cross Gateway Query/Cross Gateway Retrieve transactions.

In specific use cases, for example when a few dynamically created documents need to be accessed from interacting communities with centralized data localization; a single transaction (versus independent query and retrieve) may reduce the coordination and maintenance of the transactional dependencies and transaction states.

For such use cases, and in environments where stateless Responding Gateways can be designed, XCF simplifies the implementation of such Responding Gateways. However, it may increase the implementation complexity of Initiating Gateways serving some types of communities, such as XDS Affinity Domains. XCF offers a different deployment option from the general purpose XCA Profile.

The transaction fetches a small number of documents based upon a few retrieval parameters. This transaction is simplified to permit easier implementation and better performance on Responding Gateways.

Transcoding and translation of the documents and other data can be performed on the Responding Gateway as part of the transaction.

The XCF Profile stipulates that the following prerequisites are met:

* the document properties to be communicated are known in advance
* the result data sets can be characterized in advance
* the documents are feasible to be returned in a single response
* no further selection and/or manual interaction is needed in the communication process
* pre-conditions, such as purpose of use, legitimate data, and environment, are agreed upon in advance and are documented in a community or framework agreement
* the document fetching may not always be repeatable – it may not be assumed in every case that the same query with the same query parameters will return the same document  version with the same document id.

Ideally, only one document will satisfy the Fetch (e.g., only the most current instance of a patient summary is provided by the Responding Gateway). If the size of the set of documents matching the request is too large to be packed into a single response, an error code is returned by the Responding Gateway. The assumption is that the Cross-Community Access (XCA) Profile is used when requests are expected to return a large number of documents.

## 29.1 Actors/Transactions

Figure 29.1-1 shows the actors directly involved in the XCF Profile and the relevant transactions between them.

![alternative text](http://www.plantuml.com/plantuml/proxy?src=https://raw.github.com/plantuml/plantuml-server/master/src/main/webapp/resource/test2diagrams.txt)