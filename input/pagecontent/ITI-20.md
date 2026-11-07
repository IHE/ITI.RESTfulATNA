## 3.20 Record Audit Event [ITI-20]



### 3.20.3 Referenced Standards

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 79%" />
</colgroup>
<thead>
<tr class="header">
<th>RFC5424</th>
<th>The Syslog Protocol.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>RFC5425</td>
<td>Transmission of Syslog Messages over TLS</td>
</tr>
<tr class="even">
<td>RFC5426</td>
<td>Transmission of Syslog Messages over UDP</td>
</tr>
<tr class="odd">
<td>RFC7525</td>
<td>Recommendations for Secure Use of Transport Layer Security (TLS) and Datagram Transport Layer Security (DTLS)</td>
</tr>
<tr class="even">
<td>DICOM</td>
<td><p>DICOM PS3.15 Annex A.5</p>
<p><a href="http://medical.nema.org/medical/dicom/current/output/chtml/part15/sect_A.5.html">http://medical.nema.org/medical/dicom/current/output/chtml/part15/sect_A.</a> <a href="http://medical.nema.org/medical/dicom/current/output/chtml/part15/sect_A.5.html">5.html</a></p></td>
</tr>
<tr class="odd">
<td>ASTM E2147-01</td>
<td>Standard Specification for Audit and Disclosure Logs for Use in Health Information Systems</td>
</tr>
<tr class="even">
<td>NIST SP 800-92</td>
<td>Guide to Computer Security Log Management.</td>
</tr>
<tr class="odd">
<td>W3C XML 1.0</td>
<td>Extensible Markup Language (XML) 1.0</td>
</tr>
<tr class="even">
<td><strong>HL7 FHIR</strong></td>
<td><strong>Release 4 <a href="http://hl7.org/fhir/R4/index.html">http://hl7.org/fhir/R4/index.html</a></strong></td>
</tr>
<tr class="odd">
<td><strong>RFC4627</strong></td>
<td><strong>The application/json Media Type for JavaScript Object Notation (JSON)</strong></td>
</tr>
</tbody>
</table>

### Messages

<div style="text-align:center;">
  <img src="ITI-20.png" alt="Diagramma di interazione ITI-20" style="width:6.41975in; max-width:100%;"/>
  <p><b>Figure 3.20.4-1: Interaction Diagram</b></p>
</div>

> Note 1: Any actor initiating [ITI-20] may send to more than one Audit Record Repository.

> Note 2: The Audit Repository that receives an [ITI-20] transaction may or may not be grouped with an Audit Record Forwarder. This diagram does not show a chain of forwarding between actors.
Transaction [ITI-20] defines three different interactions that can be used for auditing:

<ol>
<li>  The "Send Audit Event Message - Syslog Interaction" is used for auditing using Syslog protocol (see Section 3.20.4.1)</li>

<li>  The "Send Audit Resource Request Message - FHIR Feed Interaction" is used for auditing a single FHIR AuditEvent Resource using RESTful protocol (see Section 3.20.4.2)</li>

<li>  The "Send Audit Bundle Request Message - FHIR Feed Interaction" is used for auditing a bundle of FHIR AuditEvent Resources using RESTful protocol (see Section 3.20.4.4)</li>
</ol>

The diagram below shows the three interactions that this transaction supports:
>
> **Secure Application, Secure Node, Audit Record Forwarder**
>
> **Audit Record Repository**
>
> **Syslog Interaction**
>
> **FHIR Feed Interaction**
>
> **FHIR Feed Interaction**

###  Messages



### 3.20.4.2 Send Audit Resource Request Message  FHIR Feed Interaction

> An actor that is grouped with Secure Node or Secure Application, or an Audit Record Forwarder, detects an event that should be reported and uses the Send Audit Resource Request message to send a report about the event to an Audit Record Repository.
>
> A Secure Node, Secure Application or Audit Record Forwarder, that supports the ATX: FHIR Feed Option, uses this message to post a single AuditEvent Resource to the Audit Record Repository using a FHIR create interaction see [https://www.hl7.org/fhir/R4/http.html#create)](https://www.hl7.org/fhir/R4/http.html#create\).

#### 3.20.4.2.1 Trigger Events

> This message is sent when an actor that is grouped with Secure Node or Secure Application or an Audit Record Forwarder needs to post a single AuditEvent Resource to the Audit Record Repository.

> There are two trigger events:

<ol>
<li>  A Secure Node or Secure Application detects an event that should be reported to the Audit Record Repository. This transaction does not specify all of the policies or reasons for reporting events. They may be specified in other IHE profiles, they may be specified by local law or regulation, or they may be specified by local policy.</li>

<li>  An Audit Record Forwarder determines that a received AuditEvent Resource should be sent to another Audit Record Repository. This transaction does not specify what rules or policies determine whether an AuditEvent Resource should be forwarded. </li>
</ol>

> An actor in any IHE profile, when grouped with a Secure Node or Secure Application, shall be able to report the events defined in Table 3.20.4.1.1.1-1. Additional reportable events are often identified for specific events in other IHE profiles, and are documented in that profile or transaction.

#### 3.20.4.2.2 Message Semantics

> A Secure Node, Secure Application or Audit Record Forwarder shall issue an HTTP request according to requirements defined in the FHIR specification for “create” interaction [(http://hl7.org/fhir/R4/http.html#create](http://hl7.org/fhir/R4/http.html#create) \). The message uses an HTTP POST method to send a FHIR AuditEvent Resource.
>
> The Secure Node, Secure Application or Audit Record Forwarder shall submit the FHIR AuditEvent Resource in either XML format or JSON format. Values for mime-type of the request message are defined in the ITI TF-2: Appendix Z.6.
>
> An AuditEvent Resource that reflect Audit Message definition defined in IHE Technical Framework shall conform to the requirements defined in Section 3.20.4.2.2.1.

##### 3.20.4.2.2.1 Mapping between DICOM Audit Message definitions and FHIR AuditEvent Resource for the FHIR Feed interactions

> The mappings between IHE defined Audit Message content and FHIR AuditEvent Resource is based on FHIR Table 6.4.7.4 [(http://hl7.org/fhir/R4/auditevent-mappings.html)](http://hl7.org/fhir/R4/auditevent-mappings.html) that is further constrained in Table 3.20.4.2.2.1-1.
>
> Table 3.20.4.2.2.1-1 is normative and contains mappings from Audit Message definitions for IHE transactions and based on DICOM standard into a FHIR AuditEvent Resource.
>
> **Table 3.20.4.2.2.1-1: DICOM Audit Message Definitions represented into an AuditEvent Resource**

<table>
<colgroup>
<col style="width: 64%" />
<col style="width: 35%" />
</colgroup>
<thead>
<tr class="header">
<th><blockquote>
<p><strong>DICOM AuditMessage</strong></p>
</blockquote></th>
<th><blockquote>
<p><strong>FHIR AuditEvent Resource</strong></p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>EventIdentification.EventID</td>
<td>type</td>
</tr>
<tr class="even">
<td>EventIdentification.EventTypeCode</td>
<td>subtype</td>
</tr>
<tr class="odd">
<td>EventIdentification@EventActionCode</td>
<td>action</td>
</tr>
<tr class="even">
<td>EventIdentification@EventDateTime</td>
<td>recorded</td>
</tr>
<tr class="odd">
<td>EventIdentification@EventOutcomeIndicator</td>
<td>outcome</td>
</tr>
<tr class="even">
<td>EventIdentification.EventOutcomeDescription</td>
<td>outcomeDesc</td>
</tr>
<tr class="odd">
<td>EventIdentification.purposeOfUse</td>
<td>purposeOfEvent</td>
</tr>
<tr class="even">
<td>ActiveParticipant</td>
<td>agent</td>
</tr>
<tr class="odd">
<td>ActiveParticipant.RoleIDCode</td>
<td>agent.type (Note 1)</td>
</tr>
<tr class="even">
<td>ActiveParticipant.RoleIDCode</td>
<td>agent.role (Note 1)</td>
</tr>
<tr class="odd">
<td>ActiveParticipant@UserId</td>
<td>agent.who</td>
</tr>
<tr class="even">
<td>ActiveParticipant@AlternativeUserId</td>
<td>agent.altId</td>
</tr>
<tr class="odd">
<td>ActiveParticipant@UserName</td>
<td>agent.name</td>
</tr>
<tr class="even">
<td>ActiveParticipant@UserIsRequestor</td>
<td>agent.requestor</td>
</tr>
<tr class="odd">
<td>ParticipantRoleIDCode</td>
<td>agent.policy</td>
</tr>
<tr class="even">
<td>ActiveParticipant.MediaIdentifier.MediaType</td>
<td>agent.media</td>
</tr>
<tr class="odd">
<td>ActiveParticipant@NetworkAccessPointID</td>
<td>agent.network.address</td>
</tr>
<tr class="even">
<td>ActiveParticipant@NetworkAccessPointTypeCode</td>
<td>agent.network.type</td>
</tr>
<tr class="odd">
<td>AuditSourceIdentification</td>
<td>source</td>
</tr>
<tr class="even">
<td>AuditSourceIdentification@AuditEnterpriseSiteId</td>
<td>source.site</td>
</tr>
<tr class="odd">
<td>AuditSourceIdentification@AuditSourceId</td>
<td>source.observer</td>
</tr>
<tr class="even">
<td>AuditSourceIdentification.AuditSourcetypeCode</td>
<td>source.type</td>
</tr>
<tr class="odd">
<td>ParticipantObjectIdentification</td>
<td>entity</td>
</tr>
<tr class="even">
<td>ParticipantObjectIdentification@ParticipantObjectID and ParticipantObjectIdentification.ParticipantObjectIDTypeCode</td>
<td>entity.what</td>
</tr>
<tr class="odd">
<td>ParticipantObjectIdentification@ParticipantObjectTypeCode</td>
<td>entity.type</td>
</tr>
<tr class="even">
<td>ParticipantObjectIdentification@ParticipantObjectTypeCodeRole</td>
<td>entity.role</td>
</tr>
<tr class="odd">
<td>ParticipantObjectIdentification@ParticipantObjectDataLifeCycle</td>
<td>entity.lifecycle</td>
</tr>
<tr class="even">
<td>ParticipantObjectIdentification@ParticipantObjectSensitivity</td>
<td>entity.securityLabel</td>
</tr>
<tr class="odd">
<td>ParticipantObjectIdentification.ParticipantObjectName</td>
<td>entity.name (Note 2)</td>
</tr>
<tr class="even">
<td>ParticipantObjectIdentification.ParticipantObjectQuery</td>
<td>entity.query (Note 2)</td>
</tr>
<tr class="odd">
<td>ParticipantObjectIdentification.ParticipantObjectDetail</td>
<td>entity.detail</td>
</tr>
<tr class="even">
<td>ParticipantObjectIdentification.ParticipantObjectDetail@type</td>
<td>entity.detail.type</td>
</tr>
<tr class="odd">
<td>ParticipantObjectIdentification.ParticipantObjectDetail@value</td>
<td>entity.detail.ValueBase64Binary</td>
</tr>
</tbody>
</table>

> Note 1: If the Audit Record Repository knows the ActiveParticipant.RoleIDCode as a type, it should be mapped to agent.type. Otherwise the default mapping is to agent.role.
>
> Note 2: Only one element between entity.name and entity.query shall be used in the AuditEvent Resource.

#### 3.20.4.2.3 Expected Actions

> The Audit Record Repository shall support all the mime-types defined in ITI TF-2: Appendix Z.6.
>
> On receipt of the Send Audit Resource Request message, the Audit Record Repository shall validate the Resources and respond with one of the HTTP codes defined in Section 3.20.4.3.2 Message Semantics.
>
> For the Resource received, the Audit Record Repository may:
<ul>
<li> discard the Resource as irrelevant </li>

<li> retain the Resource in an internal data store </li>

<li> perform other processing on the Resource </li>

</ul>

> The Audit Record Repository may apply a variety of data retention rules to the data store. This transaction does not specify data retention rules. These usually depend upon the purposes assigned to a specific Audit Record Repository.
>
> If needed, an Audit Record Repository that needs to store a received AuditEvent Resource as a DICOM Audit Message can do the transformation from the FHIR Resource to a DICOM message according to the requirements defined in Table 3.20.4.2.2.1-1.
>
> The Audit Record Repository shall store any resources that were not discarded and make them available for further search via the Retrieve ATNA Audit Event [ITI-81] transaction. These events shall not be available for further search via Retrieve Syslog Events [ITI-82] transaction.
>
> When the Audit Record Repository is grouped with an Audit Record Forwarder, the Audit Record Forwarder shall:
<ul>
<li> apply filtering rules to all AuditEvent Resources received by the Audit Record Repository, and </li>

<li> forward all AuditEvent Resources that match filters to their configured destinations. </li>
</ul>

> If needed, an Audit Record Forwarder that will forward a received AuditEvent Resource using the Audit Event message (DICOM audit event via syslog protocol) can do the transformation from the FHIR Resource to a DICOM message according to the requirements defined in Table 3.20.4.2.2.1-1.

### 3.20.4.3 Send Audit Resource Response

> The Audit Record Repository responds to the Secure Node, Secure Application or Audit Record Forwarder using a Send Audit Resource Response message in order to inform the client about the result of the operation.

#### 3.20.4.3.1 Trigger Events

> When the Audit Record Repository has finished storing the AuditEvent Resource received, it sends this message back to the client acknowledging the result of the request.

#### 3.20.4.3.2 Message Semantics

> The Audit Record Repository returns an HTTP Status code appropriate to the processing, conforming to specification requirements as specified in [https://www.hl7.org/fhir/R4/http.html#create.](https://www.hl7.org/fhir/R4/http.html#create)
>
> If the outcome is a success, the http status code of the response shall be a 2xx code.
>
> If the outcome is a failure, the Audit Record Repository shall be capable of returning status codes according to what is defined in [https://www.hl7.org/fhir/R4/http.html#create.](https://www.hl7.org/fhir/R4/http.html#create)

> The Audit Record Repository can return other status codes 4xx or 5xx in accordance to internal business rules that are out of scope for this transaction.

#### 3.20.4.3.3 Expected Actions

> The Audit Record Repository could return failures. For this reason, it is up to the client to decide what to do with failures that have been returned by the Audit Record Repository.

### 3.20.4.4 Send Audit Bundle Request Message – FHIR Feed Interaction

> A Secure Node, Secure Application or Audit Record Forwarder that supports the ATX: FHIR Feed Option uses this message to post a Bundle of AuditEvent Resources to the Audit Record Repository using a FHIR batch interaction \(see [https://www.hl7.org/fhir/R4/http.html#transaction)](https://www.hl7.org/fhir/R4/http.html#transaction).

#### 3.20.4.4.1 Trigger Events

> This message is sent when an Audit Record Forwarder or an actor that is grouped with Secure Node or Secure Application needs to send multiple events that has been audited to the Audit Record Repository.
>
> There are two trigger events:

<ol>
<li> A Secure Node or Secure Application detects at least one event that should be reported to the Audit Record Repository. This transaction does not specify all of the policies or reasons for reporting events. They may be specified in other IHE profiles, they may be specified by local law or regulation, or they may be specified by local policy.</li>

<li>  An Audit Record Forwarder determines that at least one received AuditEvent Resource should be sent to another Audit Record Repository. This transaction does not specify what rules or policies determine whether an AuditEvent Resource should be forwarded.</li>
</ol>
> An actor in any IHE profile, when grouped with a Secure Node or Secure Application, shall be able to report the events defined in Table 3.20.4.1.1.1-1. Additional reportable events are often identified for specific events in other IHE profiles, and are documented in that profile or transaction.

#### 3.20.4.4.2 Message Semantics

> An Audit Record Forwarder or an actor that is grouped with Secure Node or Secure Application shall issue an HTTP request according to requirements defined in the FHIR specification for "batch" interaction (see [https://www.hl7.org/fhir/R4/http.html#transaction)](https://www.hl7.org/fhir/R4/http.html#transaction).
>
> The Audit Record Repository and the client shall both support the "batch" interaction.
>
> The message uses an HTTP POST method to submit a FHIR Bundle Resource. The client shall post FHIR resources in either XML format or JSON format. Values for mime-type of the request message are defined in the ITI TF-2: Appendix Z.6.

> The FHIR Bundle Resource shall contain at least one FHIR AuditEvent Resource [(https://www.hl7.org/fhir/R4/auditevent.html)](https://www.hl7.org/fhir/R4/auditevent.html).
>
> The element Bundle.entry.request.method shall be POST.
>
> AuditEvent Resources included in the Bundle that reflect Audit Message definitions defined in IHE Technical Framework shall conform to the requirements defined in Section 3.20.4.2.2.1.

**Table 3.20.4.4.2-1: Bundle Resource Constraints**

<table>
<colgroup>
<col style="width: 45%" />
<col style="width: 54%" />
</colgroup>
<thead>
<tr class="header">
<th><blockquote>
<p><strong>Element &amp;</strong></p>
</blockquote>
<p><strong>Cardinality</strong></p></th>
<th><strong>Constraints</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>type [1..1]</td>
<td>Shall be: batch</td>
</tr>
<tr class="even">
<td>entry [1..*]</td>
<td>Shall contain at least one AuditEvent Resource.</td>
</tr>
<tr class="odd">
<td>entry.request.method</td>
<td>Shall be: POST</td>
</tr>
</tbody>
</table>

#### 3.20.4.4.3 Expected Actions

> The Audit Record Repository shall support all the mime-types defined in ITI TF-2: Appendix Z.6.
>
> On receipt of the Send Audit Bundle Resource Request, the Audit Record Repository shall validate Resources included in it and respond with one of the HTTP codes defined in Section
>
> #### 3.20.4.5.2 Message Semantics
>
> For each Resource received in the Bundle, the Audit Record Repository may:

<ul>
<li> Discard the Resource as irrelevant. </li>

<li> Retain the Resource in an internal data store. </li>

<li> Perform other processing on the Resource. </li>
</ul>

> The Audit Record Repository may apply a variety of data retention rules to the data store. This transaction does not specify data retention rules. These are usually dependent upon the purposes assigned to a specific Audit Record Repository.
>
> If needed, an Audit Record Repository that needs to store a received AuditEvent Resource as a DICOM Audit Message can do the transformation from the FHIR Resource to a DICOM message according to the requirements defined in Table 3.20.4.2.2.1-1.
>
> The Audit Record Repository shall store any resources that were not discarded and make them available for further search via the Retrieve ATNA Audit Event [ITI-81] transaction. These events shall not be available for further search via Retrieve Syslog Events [ITI-82] transaction.

> When the Audit Record Repository is grouped with an Audit Record Forwarder, the Audit Record Forwarder shall:

<ul>

<li> Apply filtering rules to all AuditEvent Resources received by the Audit Record Repository, and </li>

<li> Forward all AuditEvent Resources that match filters to their configured destinations. </li>

</ul>

> If needed, an Audit Record Forwarder that needs to forward a received AuditEvent Resource using the Audit Event message can do the transformation from the FHIR Resource to a DICOM message according to the requirements defined in Table 3.20.4.2.2.1-1.

### 3.20.4.5 Send Audit Bundle Response

> The Audit Record Repository sends a Send Audit Bundle Response message in response to a Send Audit Bundle Request.

#### 3.20.4.5.1 Trigger Events

> When the Audit Record Repository has finished storing the AuditEvent Resources received in the Bundle Resource, it sends back this message to the client acknowledging the result of the request.

#### 3.20.4.5.2 Message Semantics

> The Audit Record Repository returns an HTTP Status code appropriate to the processing, conforming to specification requirements as specified in [https://www.hl7.org/fhir/R4/http.html#transaction-response.](https://www.hl7.org/fhir/R4/http.html#transaction-response)
>
> When the Audit Record Repository has processed the request shall return an HTTP response with an overall status code.
>
> To allow the client to know the outcome of the transaction, and the identities assigned to the resources by the Audit Record Repository, the Audit Record Repository shall return a Bundle, with type set to batch-response. Each entry element shall contain a response element with an HTTP Status Code which details the outcome of processing of the request entry.
>
> If no "Prefer" header is specified in the request the server should respond as if it is set to
>
> return=minimal; see [https://www.hl7.org/fhir/R4/http.html#ops.](https://www.hl7.org/fhir/R4/http.html#ops)
>
> If the outcome of the entry is a success, the http status code of the response shall be a 2xx code.
>
> If the outcome of the entry is a failure, the Audit Record Repository shall be capable of returning status codes according to what is defined in [https://www.hl7.org/fhir/R4/http.html#create.](https://www.hl7.org/fhir/R4/http.html#create)
>
> The Audit Record Repository can return other status codes 4xx or 5xx in accordance to internal business rules that are out of scope for this transaction.

#### 3.20.4.5.3 Expected Actions

> The Audit Record Repository could return a partial success for the Bundle where some resources succeeded and other not. For this reason, it is up to the client to decide what to do with failures that have been returned by the Audit Record Repository.

### 3.20.5 Security Considerations

> The use of the TLS **or HTTPS** transport mechanism<img src="media/image7.png" />is recommended because the audit event messages often contain PHI or other sensitive information. See [Section 3.20.4.1.2.1.](https://profiles.ihe.net/ITI/TF/Volume2/ITI-20.html#3.20.4.1.2.1)
>
> The use of the TLS transport mechanism is not always required because there are other means of protection that may be more appropriate in some situations. The decision to use the UDP transport mechanism should be based upon a security and privacy risk analysis.
>
> The data store within the Audit Record Repository may contain sensitive information, and the Audit Record Repository analysis facilities may allow sensitive queries. It will be a high value target for malicious actors, and should be protected accordingly.
>
> The Audit Record Repository is required to generate audit event messages for various kinds of use of the data store and configuration changes. This is specified in [Section 3.20.4.1.1.](https://profiles.ihe.net/ITI/TF/Volume2/ITI-20.html#3.20.4.1.1.1)

If the AuditEvent Message Option is supported on the Audit Record Repository, update, delete and patch interaction of AuditEvent Resources should be managed by local policies.