<a name="actors-and-transactions"> </a>

## 1:XX.1 Actors, Transactions, and Content Modules

This section defines the actors and transactions in this implementation guide.

* Actors
  * [Audit Record Repository](#ARR)
  * [Audit Consumer](#AC)
  * [Audit Record Forwarder](#ARF)
  * [Secure Node](#SN)
  * [Secure Application](#SA)
* Transactions
  * [Record Audit Event [ITI-20]](ITI-20.html)
  * [Retrieve ATNA Audit Event [ITI-81]](ITI-81.html)
  * [Retrieve Syslog Event [ITI-82]](ITI-82.html)

The figure below shows the actors directly involved in the RESTfulAtna Profile and the relevant transactions between them.

<figure>
{%include ActorsAndTransactions.svg%}
<figcaption><strong>Figure 1:XX.1-2: RESTful ATNA Actor Diagram</strong></figcaption>
</figure>
<br clear="all">

<p id ="tXX.1-1" class="tableTitle"><strong>Table 1:XX.1-1: RESTful ATNA - Actors and Transactions</strong></p>

| Actors                  | Transactions                       | Optionality | Reference      |
|-------------------------|------------------------------------|-------------|----------------|
| Audit Record Repository | Record Audit Event [ITI-20]        | R           | ITI TF-2: 3.20 |
|                         | Retrieve ATNA Audit Event [ITI-81] | O           | ITI TF-2: 3.81 |
|                         | Retrieve Syslog Event [ITI-82]     | O           | ITI TF-2: 3.82 |
| Audit Consumer          | Retrieve ATNA Audit Event [ITI-81] | O           | ITI TF-2: 3.81 |
|                         | Retrieve Syslog Event [ITI-82]     | O           | ITI TF-2: 3.82 |
| Audit Record Forwarder  | Record Audit Event [ITI-20]        | R           | ITI TF-2: 3.20 |
| Secure Node             | Authenticate Node [ITI-19]         | R           | ITI TF-2: 3.19 |
|                         | Record Audit Event [ITI-20]        | R           | ITI TF-2: 3.20 |
| Secure Application      | Authenticate Node [ITI-19]         | R           | ITI TF-2: 3.19 |
|                         | Record Audit Event [ITI-20]        | R           | ITI TF-2: 3.20 |

### 1:XX.1.1 Actors
The actors in this profile are described in more detail in the sections below.
#### 1:XX.1.1.1 Audit Record Repository

> The Audit Record Repository receives event audit reports and stores
> them. It may be part of a federated network of repositories. It is
> expected to have analysis and reporting capabilities, but those
> capabilities are not specified as part of this profile. This profile
> does not specify the capacity of an Audit Record Repository, because
> the variety of deployment needs makes it impractical to set
> requirements for the event report volume or capacity needed.
>
> The Audit Repository shall support:
<ol>
  <li>At least one of the audit transport mechanisms specified in [ITI
    TF-2: 3.20](https://profiles.ihe.net/ITI/TF/Volume2/ITI-20.html)
    (see Table 9.2-1).</li>
  <li>Receipt of at least one of the IHE-specified audit message formats.
    Note that the message format is extensible to include both future
    IHE specifications (e.g., audit requirements for new IHE
    transactions) and private extensions.</li>
  <li>Local security and privacy service protections and user access
    controls.</li>
</ol>

> The Audit Record Repository may ignore or process messages in non-IHE message formats. This may be for backwards compatibility or other reasons.
> The Audit Record Repository be grouped with a Secure Node or Secure Application.
> The Audit Record Repository may support search capabilities as defined in ITI TF-2: 3.81 and 3.82.
> Audit Record Repository may support search capabilities as defined in ITI TF-2: 3.81 and 3.82.

#### 1:XX.1.1.2 Audit Consumer

> The Audit Consumer queries an Audit Record Repository for syslog and
> ATNA audit records using Syslog metadata and ATNA audit record
> content. Subsequent processing of the query result is not defined in this profile.

<a name="actor-options"> </a>

## 1:XX.2 Actor Options

> Options that may be selected for this Integration Profile are listed
> in the Table 9.2-1 along with the actors to which they apply.
> Dependencies between options when applicable are specified in notes.
>
> Note: The "ATX" prefix in option names below marks alternatives for
> audit transport protocol, and the "STX" prefix marks alternatives for
> secure transport protocol, as defined in the Record Audit Event
> \[ITI-20\] transaction.

<p id ="tXX.2-1" class="tableTitle"><strong>Table 1:XX.2-1: ATNA - Actors and Options</strong></p>

| Actor                            | Option Name                      | Vol. & Section    |
|----------------------------------|----------------------------------|-------------------|
| Audit Record Repository (Note 4) | Retrieve Audit Message           | ITI TF-1: 9.2.3   |
|                                  | Retrieve Syslog Message          | ITI TF-1: 9.2.4   |
|                                  | ATX: FHIR Feed                   | ITI TF-1: 9.2.7.1 |
|                                  | ATX: TLS Syslog                  | ITI TF-1: 9.2.7.2 |
|                                  | ATX: UDP Syslog                  | ITI TF-1: 9.2.7.3 |
| Audit Consumer                   | Retrieve Audit Message (Note 5)  | ITI TF-1: 9.2.3   |
|                                  | Retrieve Syslog Message (Note 5) | ITI TF-1: 9.2.4   |
| Audit Record Forwarder (Note 4)  | ATX: FHIR Feed                   | ITI TF-1: 9.2.7.1 |
|                                  | ATX: TLS Syslog                  | ITI TF-1: 9.2.7.2 |
|                                  | ATX: UDP Syslog                  | ITI TF-1: 9.2.7.3 |
| Secure Node (Note 1)             | Radiology Audit Trail            | RAD TF-1: 2.2.1   |
| (Note 4)                         |                                  | RAD TF-3: 5.1     |
|                                  | ATX: FHIR Feed                   | ITI TF-1: 9.2.7.1 |
|                                  | ATX: TLS Syslog                  | ITI TF-1: 9.2.7.2 |
|                                  | ATX: UDP Syslog                  | ITI TF-1: 9.2.7.3 |
| Secure Application (Note 1)      | Radiology Audit Trail            | RAD TF-1: 2.2.1   |
| (Note 4)                         |                                  | RAD TF-3: 5.1     |
{: .grid}

> Note 4: This actor shall support at least one of the "ATX" Options. If a product's IHE Integration Statement does not declare one of these options, the reader should assume that the product supports the TLS or UDP Syslog Option.

> Note 5: The Audit Consumer shall support at least one of the two options defined.

###  1:XX.2.1 Retrieve Audit Message Option

> The Retrieve Audit Message Option enables search requests for audit records based upon message contents.
> An Audit Consumer or Audit Record Repository that supports this option shall implement the Retrieve ATNA Audit Event \[ITI-81\] transaction.
> The \[ITI-81\] transaction is a RESTful search from an Audit Consumer to an Audit Record Repository (ARR) using FHIR resources. The search response will reflect the contents of the data storage at the time of the search. IHE does not specify the criteria for message selection, archival, retention interval, etc. These are set by local policy and are often different for different Audit Record Repositories.

### 1:XX.2.2 Retrieve Syslog Message Option

> The Retrieve Syslog Message Option enables search requests for syslog messages based upon syslog metadata.
> An Audit Consumer or Audit Record Repository that supports this option shall implement the Retrieve Syslog Event \[ITI-82\] transaction.
> The \[ITI-82\] transaction is a RESTful search operation that searches syslog messages of any format or schema. The search request uses the syslog metadata only.

### 1:XX.2.3 Audit Transport (ATX) Options

> At least one of these options shall be supported. Many can be declared, for which the productmust then be configurable to enable each of the supported Audit Transport Options.

#### 1:XX.2.3.1 ATX: FHIR Feed Option

> The ATX: FHIR Feed Option enables sending ATNA audit records using RESTful capabilities and FHIR resources.
> An Audit Record Repository that supports this option shall implement the two RESTful interactions defined in the Record Audit Event \[ITI-20\] transaction. See ITI TF-2: 3.20.4.2 (Send Audit Resource) and 3.20.4.4 (Send Audit Bundle).
> A Secure Node, Secure Application or Audit Record Forwarder that supports this option shall at least support one of the two RESTful interactions defined in the Record Audit Event \[ITI-20\] transaction. See ITI TF-2: 3.20.4.2 (Send Audit Resource) and 3.20.4.4 (Send Audit Bundle).

> #### 1:XX.2.3.2 ATX: TLS Syslog Option

<p id ="1:XX.2.3.2-1" class="tableTitle"><strong>Table 1:XX.2.3.2-1: ATNA - Required Actor Groupings</strong></p>

| ATNA Actor              | Actor to be grouped with               | Reference   | Content Bindings Reference |
|-------------------------|----------------------------------------|-------------|----------------------------|
| Audit Record Repository | Consistent Time/Time Client            | ITI TF-1: 7 | N/A                        |
|                         | ATNA/Secure Node or Secure Application | ITI TF-1: 9 | N/A                        |
| Audit Consumer          | ATNA/Secure Node or Secure Application | ITI TF-1: 9 | N/A                        |
{: .grid}

<a name="use-cases"> </a>

## 1:XX.3 Use Cases
> Sections 9.4.2.1, 9.4.2.2, and 9.4.2.3 describe three typical process flows for situations in which authorized users, unauthorized users, and unauthorized nodes attempt to gain access to protected health information (PHI).
> Sections 9.4.2.4 and 9.4.2.5 describe use cases related to the retrieve capabilities of the Audit Record Repository.

### 1:XX.3.1 Clinician Personal History of Study views Process Flow
A clinician wants to gather the history of studies she has accessed during her clinical activity using different devices (EHR system, WebApp, Mobile device). This information allows the clinician to:
<ul>
  <li>Discover unexpected accesses made to her devices;</li>
  <li>Re-evaluate clinical decisions taken;</li>
  <li>Consolidate on a unique device, a complete picture of complex clinical cases.</li>
</ul>

#### 1:XX.3.1.1 Clinician Personal History of Study views use-case

Dr. Luisa White usually performs her clinical activity using multiple devices. Mr. Brown is a patient who is home-monitored. Dr. White collects results of home visits using a tablet, and she monthly performs a detailed visit with Mr. Brown in her office. During home visits, Dr. White analyzes tele-monitoring data collected by some devices (scales, blood pressure devices, etc.) and adjusts drugs therapies in accordance with those data. When Dr. White accesses Mr.
Brown’s data via these devices, each access is tracked as an ATNA audit event. Both document views and document creation are logged, tracking the user that performed the transaction (e.g., using an XUA identity assertion).
Monthly visit, Dr. White wants to consolidate within her EHR system the whole history of data analyzed and collected using multiple devices. This process allows Dr. White to keep track of her clinical activities and revaluate clinical decisions made in the past.
To facilitate that, the EHR system can query for audit events related to transactions performed by Dr. White during a specific period.

<figure>
  <img src="Untitled4.png" alt="Clinician Personal History of Study views Process Flow" style="width:100%"/>
  <figcaption><b>1:XX.3.1.1-1: Clinician Personal History of Study views Process Flow</b></figcaption>
</figure>

### 1:XX.3.2 Patient access to his audit records Process Flow
A patient wants to discover the list of people that accessed a specific study. Using those data, the patient discovers if privacy policies were correctly applied.

<figure>
  <img src="usecase2.svg" alt="Patient access to his audit records Process Flow"/>
  <figcaption><b>1:XX.3.2-1: Patient access to his audit records Process Flow</b></figcaption>
</figure>

#### 1:XX.3.2.1 Patient access to his audit records use case
During a hospitalization, Mr. Brown was asked to sign a consent to share documents produced during that clinical event with a research facility, so that researchers could analyze the efficiency of the applied treatment. Mr. Brown does not provide this consent because he is worried that his data could be used for marketing purposes. A nurse collects the patient’s consent document, but forgets to record his decision in the HIS system.
Access to all the data collected during Mr. Brown’s hospitalization by clinicians involved in his care are tracked as “Export” or “Disclosure events for a “Treatment” purpose. An access to the data by the research facility would be tracked as “Export” or “Disclosure” events for a “Research” purpose. Mr. Brown’s healthcare facility provides on-line access to health information. Mr. Brown can use a web app to access this data (shared using XDS or XCA infrastructure). The web app can also display audit information related to those documents/studies. Audit records are collected by many ATNA Audit Record Repositories, but local policies or system configurations allows the web app to identify the right Audit Record Repository system that stores relevant records. Using the document and study identifiers, the web app can query the appropriate ATNA Audit Record Repository.
The web app reports to Mr. Brown that his documents/studies had been disclosed or exported for both treatment and research purposes.


<a name="security-considerations"> </a>

## 1:XX.4 ToDo Security Considerations

See ITI TF-2: [Appendix Z.8 "Mobile Security Considerations"](https://profiles.ihe.net/ITI/TF/Volume2/ch-Z.html#z.8-mobile-security-considerations)

The following is instructions to the editor and this text is not to be included in a publication.
The material initially from [RFC 3552 "Security Considerations Guidelines" July 2003](https://tools.ietf.org/html/rfc3552).

This section should address downstream design considerations, specifically for: Privacy, Security, and Safety. These might need to be individual header sections if they are significant or need to be referenced.

The editor needs to understand Security and Privacy fundamentals.
General [Security and Privacy guidance]({{site.data.fhir.path}}secpriv-module.html) is provided in the FHIR Specification. 
The FHIR core specification should be leveraged where possible to inform the reader of your specification.

IHE FHIR based profiles should reference the [ITI Appendix Z](https://profiles.ihe.net/ITI/TF/Volume2/ch-Z.html) section 8 Mobile Security and Privacy Considerations base when appropriate.

IHE Document Content profiles can reference the security and privacy provided by the Document Sharing infrastructure as directly grouped or possibly to be grouped.

   While it is not a requirement that any given specification or system be
   immune to all forms of attack, it is still necessary for authors of specifications to
   consider as many forms as possible.  Part of the purpose of the
   Security and Privacy Considerations section is to explain what attacks have been
   considered and what countermeasures can be applied to defend against them.

   There should be a clear description of the kinds of threats on the
   described specification.  This should be approached as an
   effort to perform "due diligence" in describing all known or
   foreseeable risks and threats to potential implementers and users.

Authors MUST describe:

- which attacks have been considered and addressed in the specification
- which attacks have been considered but not addressed in the specification
- what could be done in system design, system deployment, or user training

   At least the following forms of attack MUST be considered:
   eavesdropping, replay, message insertion, deletion, modification, and
   man-in-the-middle.  Potential denial of service attacks MUST be
   identified as well.  If the specification incorporates cryptographic
   protection mechanisms, it should be clearly indicated which portions
   of the data are protected and what the protections are (i.e.,
   integrity only, confidentiality, and/or endpoint authentication,
   etc.).  Some indication should also be given to what sorts of attacks
   the cryptographic protection is susceptible.  Data which should be
   held secret (keying material, random seeds, etc.) should be clearly
   labeled.

   If the specification involves authentication, particularly user-host
   authentication, the security of the authentication method MUST be
   clearly specified.  That is, authors MUST document the assumptions
   that the security of this authentication method is predicated upon.

   The threat environment addressed by the Security and Privacy Considerations
   section MUST at a minimum include deployment across the global
   Internet across multiple administrative boundaries without assuming
   that firewalls are in place, even if only to provide justification
   for why such consideration is out of scope for the protocol.  It is
   not acceptable to only discuss threats applicable to LANs and ignore
   the broader threat environment.  In
   some cases, there might be an Applicability Statement discouraging
   use of a technology or protocol in a particular environment.
   Nonetheless, the security issues of broader deployment should be
   discussed in the document.

   There should be a clear description of the residual risk to the user
   or operator of that specification after threat mitigation has been
   deployed.  Such risks might arise from compromise in a related
   specification (e.g., IPsec is useless if key management has been
   compromised), from incorrect implementation, compromise of the
   security technology used for risk reduction (e.g., a cipher with a
   40-bit key), or there might be risks that are not addressed by the
   specification (e.g., denial of service attacks on an
   underlying link protocol).  Particular care should be taken in
   situations where the compromise of a single system would compromise
   an entire protocol.  For instance, in general specification designers
   assume that end-systems are inviolate and don't worry about physical
   attack.  However, in cases (such as a certificate authority) where
   compromise of a single system could lead to widespread compromises,
   it is appropriate to consider systems and physical security as well.

   There should also be some discussion of potential security risks
   arising from potential misapplications of the specification or technology
   described in the specification.  
  
This section also include specific considerations regarding Digital Signatures, Provenance, Audit Logging, and De-Identification.

Where audit logging is specified, a StructureDefinition profile(s) should be included, and Examples of those logs might be included.
