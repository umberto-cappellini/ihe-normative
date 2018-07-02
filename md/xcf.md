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

![Figure 29.1-1](http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/umberto-cappellini/ihe-normative/master/uml/xcf_actor_diagram.uml?version=201807271630)

Table 29.1-1 lists the transactions for each actor directly involved in the XCF Profile. In order to claim support of this profile, an implementation must perform the required transactions (labeled “R”). Transactions labeled “O” are optional. A complete list of options defined by this profile and that implementations may choose to support is listed in Section 29.2.

Table 29.1-1: XCF Profile - Actors and Transactions

| Actors | Transactions | Optionality | Reference |
| :--- | :--- | :---: | :--- |
| Initiating Gateway  | Cross Gateway Fetch [ITI-63] | R | ITI TF-2b: 3.63 |
| Responding Gateway  | Cross Gateway Fetch [ITI-63] | R | ITI TF-2b: 3.63 |

## 29.2 XCF Profile Options

Options that may be selected for this profile are listed in the Table 29.2-1 along with the actors to which they apply. Dependencies between options when applicable are specified in notes.

Table 29.2-1: XCF - Actors and Options

| Actors | Options | Reference |
| :--- | :--- | :---: |
| Initiating Gateway  | Asynchronous Web Services Exchange | Section 29.2.1 |
| Responding Gateway  | No options defined | -- |

The Responding Gateways shall support Asynchronous Web Services Exchange Option on the Cross Gateway Fetch. Support for this function is required in order to enable use of Asynchronous Web Services Exchange in any cross-community interaction.

### 29.2.1 Asynchronous Web Services Exchange Option

Initiating Gateways which support Asynchronous Web Services Exchange shall support Asynchronous Web Services Exchange on the Cross Gateway Fetch [ITI-63] transaction.

## 29.3 XCF Actor Groupings and Profile Interactions

### 29.3.1 XCF Required Groupings

An actor from this profile (Column 1) shall implement all of the required transactions and/or content modules in this profile in addition to all of the transactions required for the grouped actor (Column 2).

If this is a content profile, and actors from this profile are grouped with actors from a workflow or transport profile, the Content Bindings reference column references any specifications for mapping data from the content module into data elements from the workflow or transport transactions.

Table 29.3.1-1: XCF - Required Actor Groupings

| XCF Actor | Actor to be grouped with | Reference | Content Bindings Reference |
| :--- | :--- | :---: | :--- |
| Initiating Gateway  | ATNA / Secure Node or Secure Application | ITI TF-1: 9 | -- |
|   | CT / Time Client | ITI TF-1: 7 | -- |
|   | XUA / X-Service User | ITI TF-1: 13 | -- |
| Responding Gateway  | ATNA / Secure Node or Secure Application | ITI TF-1: 9 | -- |
|   | CT / Time Client | ITI TF-1: 7 | -- |
|   | XUA / X-Service User | ITI TF-1: 13 | -- |

### 29.3.2 XDS/XCA Interactions (Informative)

Interoperable interaction between communities which have chosen to implement only XCF and those that are based on XDS or XCA may be enabled through transformation agents. IHE does not specify the mechanism used by such transformation agents or any details about their implementation. The following sections give a high level perspective on the challenges of enabling four cases of agents:

1. “responding agent” for XDS- acts as an XCF Responding Gateway and converts incoming Cross Gateway Fetch transactions into XDS transactions to collect the content needed for the response.
2. “responding agent” for XCA- acts as an XCF Responding Gateway and converts incoming Cross Gateway Fetch transactions into XCA transactions to collect the content needed for the response.
3. “initiating agent” for XDS – acts as an XCF Initiating Gateway and converts XDS transactions into Cross Gateway Fetch transactions to collect content from XCF only communities.
4. “initiating agent” for XCA– acts as an XCF Initiating Gateway and converts XCA transactions into Cross Gateway Fetch transactions to collect content from XCF only communities.

Some agents are relatively easy to implement and others are quite complicated. In environments where integration of with XCA and XDS is important it would be advisable to consider XCA with the On-Demand Documents Option as an alternative to the use of XCF.

### 29.3.2.1 “responding agent” for XDS (Grouping with Document Consumer)

A “responding agent” for XDS converts incoming Cross Gateway Fetch transactions into Registry Stored Query [ITI-18] and Retrieve Document Set [ITI-43] transactions which are directed to a local XDS Registry/Repository. This type of agent has value because it allows access by XCF only communities to content within XDS based communities.

A “responding agent” for XDS can be enabled through a relatively simple grouping of XDS Document Consumer and XCF Responding Gateway. The agent must convert the Cross Gateway Fetch query into a collection of Registry Stored Query and Retrieve Document Set transactions.
This conversion is relatively straightforward; the query in the Cross Gateway Fetch transaction maps closely to the Find Documents stored query of Registry Stored Query and from this query the agent can generate appropriate Retrieve Document Set transactions to get the document contents. Several additional details need to be managed by the agent, like supplying document associations and handling situations when the results are too large to be returned in the Cross Gateway Fetch response. Figure 29.3.2.1-1 depicts this environment.

![Responding Agent](../img/responding_agent.png)

### 29.3.2.2 “responding agent” for XCA
