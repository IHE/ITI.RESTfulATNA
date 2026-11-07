## 3.81 Retrieve ATNA Audit Event [ITI-81]

> This transaction supports the retrieval of ATNA audit record from the Audit Record Repository in accordance with a set of search parameters that determine the retrieved event reports. This transaction enables an Audit Consumer to search audit events that an Audit Record Repository created via the Record Audit Event [ITI-20] transaction.
>
> This transaction is a profiling of a standard FHIR search of the AuditEvent Resource.

### 3.81.1 Scope

> The Retrieve ATNA Audit Event transaction is used to search ATNA events recorded in an ATNA Audit Record Repository. The result of this retrieval is a FHIR bundle of AuditEvent Resources that match with a set of search parameters.

### 3.81.2 Actor Roles

> **Table 3.81.2-1: Actor Roles**

| **Actor:** | Audit Record Repository                                                                              |
|------------|------------------------------------------------------------------------------------------------------|
| **Role:**  | Provides storage for ATNA audit events, and responds to queries for a portion of the stored records. |
| **Actor:** | Audit Consumer                                                                                       |
| **Role:**  | Queries for ATNA audit records.                                                                      |

### 3.81.3 Referenced Standards

<table>
<colgroup>
<col style="width: 5%" />
<col style="width: 22%" />
<col style="width: 71%" />
</colgroup>
<thead>
<tr class="header">
<th>885</th>
<th><blockquote>
<p>RFC2616</p>
</blockquote></th>
<th>IETF Hypertext Transfer Protocol – HTTP/1.1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td></td>
<td><blockquote>
<p>RFC4627</p>
</blockquote></td>
<td>The application/json Media Type for JavaScript Object Notation (JSON)</td>
</tr>
<tr class="even">
<td></td>
<td>RFC6585</td>
<td>IETF Additional HTTP Status Codes</td>
</tr>
<tr class="odd">
<td></td>
<td>RFC5424</td>
<td>The Syslog Protocol</td>
</tr>
<tr class="even">
<td></td>
<td>RFC3339</td>
<td>Date and Time on the Internet: Timestamps</td>
</tr>
<tr class="odd">
<td><p>HL7 FHIR</p>
<blockquote>
<p><strong>
</strong></p>
</blockquote></td>
<td>Release 4 <a href="http://hl7.org/fhir/R4/index.html">http://hl7.org/fhir/R4/index.html</a></td>
</tr>
</tbody>
</table>

> ### 3.81.4 Messages

>
> **Figure 3.81.4-1: Interaction Diagram**

#### 3.81.4.1  Retrieve ATNA Audit Events Message

> This is an HTTP GET parameterized search from an Audit Consumer to an Audit Record Repository. The Audit Record Repository has stored ATNA audit records received via Record Audit Event [ITI-20] transactions. Those messages, which are stored within a data-store, can be retrieved in accordance with specific search parameters.

##### 3.81.4.1.1 Trigger Events

> The Audit Consumer sends a Retrieve ATNA Audit Events message when it needs to process or analyze ATNA audit records.

##### 3.81.4.1.2 Message Semantics

> The Retrieve ATNA Audit Event message shall be an HTTP GET request sent to the Audit Record Repository. This message is a FHIR search (see [http://hl7.org/fhir/R4/search.html)](http://hl7.org/fhir/R4/search.html) on AuditEvent Resources (see [http://hl7.org/fhir/R4/auditevent.html)](http://hl7.org/fhir/R4/auditevent.html). This “search” target is formatted as:
>
> `\<scheme\>://\<authority\>/\<path\>/AuditEvent?date=ge[start-time]&date=le[stop-time]&\<query\>`
>
> where:
<ul>
<li> `<scheme>` shall be either http or https. The use of http or https is a policy decision, but https is usually appropriate due to confidentiality of ATNA audit record content </li>

<li> `<authority>` shall be represented as a host (either IP address or DNS name) followed optionally by a colon and port number </li>

<li> The Audit Record Repository may use \<path\> to segregate the HTTP search service for AuditEvent implementation from other REST-based services </li>

<li> At least one date search parameter is required. See Section 3.81.4.1.2.1 </li>

<li> **“&”** is a conditional parameter that shall be present if the \<query\> parameter is present </li>

<li> \<query\>, if present, represents a series of encoded name-value pairs representing filters for the search. See Section 3.81.4.1.2.2 </li>

</ul>

###### 3.81.4.1.2.1 Date Search Parameters

> The date parameter shall be used to specify an upper and/or lower bound for the search. At least one date parameter shall be present. Two date parameters are recommended in every search by the Audit Consumer and shall be supported by the Audit Record Repository in order to avoid overloading the Audit Consumer. These parameters allow the Audit Consumer to specify the time frame of creation of audit records of interest and enable the Audit Consumer to constrain
>
> the number of audit records returned. The values for the date search parameters shall be in RFC3339 format.
>
> Note: RFC3339 format is the format mandated by Syslog for time stamps and is a sub-set of the XML date-time data format used by FHIR.
>
> For example, to search AuditEvent Resources created during the whole day of January 5, 2013:
>
> <http://example.com/ARRservice/AuditEvent?date=ge2013-01-05&date=le2013-01-05>

> The Audit Record Repository shall apply matching criteria to AuditEvent Resources characterized by AuditEvent.recorded field valued within the time frame specified in the Request message.
>
> The Audit Record Repository shall apply other date matching criteria following rules defined by FHIR specification [(http://hl7.org/fhir/R4/search.html)](http://hl7.org/fhir/R4/search.html).

###### 3.81.4.1.2.2 Additional ATNA Search Parameters

> The search parameters in this section may be supported by the Audit Consumer and shall be supported by the Audit Record Repository. These parameters can be used by the Audit Consumer to refine search requests. Refer to Section 3.81.4.2.2 for the mapping between the FHIR AuditEvent Resource and the DICOM standard definition.
>
> The Audit Consumer shall encode all search parameters per RFC3986 “percent” encoding rules. Although FHIR allows unconstrained use of AND OR operators to make queries of unlimited complexity, this transaction constrains the queries allowed:

<ul>
<li> Multiple search parameters shall only be combined using AND **“&”** operator </li>

<li> The OR **“,”** operator shall be used only within a single search parameter that has multiple values </li>

</ul>

> Additional search parameters are listed below:

<ul>
<li>
 address is a parameter of string type. This parameter specifies the identifier of the network access point (NetworkAccessPointID) of the user device that creates the audit record (this could be a device id, IP address, or some other identifier associated with a device).


> The value of this parameter shall contain the substring to match.

> For example:
>
> <http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013-01-02&address=192.168.0.1>
>
> The Audit Record Repository shall match this parameter with the
>
> AuditEvent.agent.network.address. </li>

<li> agent.identifier is a parameter of token type. This parameter identifies the user that participated in the event that originates the audit record. 

> For example, to search AuditEvent Resources related to the user “admin”:
>
> <http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013-01-02&agent.identifier=admin>

> The Audit Record Repository shall match this parameter with the
>
> AuditEvent.agent.who.identifier field.
>
> If a patient identifier it is used, the Audit Record Repository will return only the audit records where the patient is involved in the event as a user.</li>

<li> patient.identifier is a parameter of token type. This parameter specifies the identifier of the patient involved in the event as a participant or as a user. The value of this parameter can contain the namespace URI (that represents the assigning authority for the identifier) and the identifier.

> For example:
>
> [http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013-01-02&patient.identifier=urn:oid:1.2.3.4](http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013-01-02&patient.identifier=urn%3Aoid%3A1.2.3.4)\|5678

> The Audit Record Repository shall match this parameter with the AuditEvent.agent.who.identifier and AuditEvent.entity.what.identifier where the reference resolve to a Patient. </li>

<li> entity.identifier is a parameter of token type. This parameter specifies unique identifier for the object. The parameter value should be identified in accordance to the entity type.

> For example:
<ul>
<li> ?entity.identifier=urn:oid:1.2.3.4.5\|123-203-FJ </li>

<li> ?entity.identifier=\|123-203-FJ. </li>


> The Audit Record Repository shall match this parameter with the AuditEvent.entity.what.identifier field that is of type identifier (ParticipantObjectID in DICOM schema). If a patient identifier is used the Audit Record Repository will return only audit records where the patient is involved in the event as a participant. </li>

<li> entity-type is a parameter of token type. This parameter specifies the type of the object (e.g., Person, System Object, etc.). The parameter value shall contain the CodeSystem namespace URI <http://terminology.hl7.org/CodeSystem/audit-entity-type> or <http://hl7.org/fhir/resource-types> defined by FHIR and a coded value. See [http://hl7.org/fhir/R4/valueset-audit-entity-type.html](http://hl7.org/fhir/R4/valueset-audit-entity-type.html) for codes that shall be used.


> The Audit Record Repository shall match this parameter with the
>
> AuditEvent.entity.type field. </li>

<li> entity-role is a parameter of token type. This parameter specifies the role played by the entity (e.g., Report, Location, Query, etc.). The parameter value shall contain the namespace URI <http://hl7.org/fhir/object-role> defined by FHIR and a coded value. See [http://hl7.org/fhir/R4/object-role](http://hl7.org/fhir/R4/object-role) for codes that shall be used.

> For example, to search all the audit records related to the document entity (Report=”3”) with the unique id 12345^1.2.3.4.5 a fully specified request would be:
>
> [http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013-01-02&entity-role=http://hl7.org/fhir/object-role](http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013-01-02&entity-role=http%3A//hl7.org/fhir/object-role)\|3&entity-id=urn:oid:1.2.3.4.5\|12345
>
> The Audit Record Repository shall match this parameter with the
>
> AuditEvent.entity.role field. </li>

<li> source.identifier is a parameter of token type. This parameter identifies the source of the audit event (DICOM AuditSourceID).

> For example, to search AuditEvent Resources produced by the audit source application characterized by unique ID: 1234:
>
> <http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013-01-02&source=1234>

> The Audit Record Repository shall match this parameter with the
>
> AuditEvent.source.observer.identifier field. </li>

<li> type is a parameter of token type. This parameter represents the identifier of the specific type of event audited. The parameter value shall contain the namespace URI <http://dicom.nema.org/resources/ontology/DCM> and a coded value. Codes available are defined by DICOM and IHE (see ITI TF-1: Table 3.20.4.1.1.1-1: Audit Record trigger events).

> For example, to search AuditEvent Resources related to PHI Export Events:
>
> [http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013-01-02&type=http://dicom.nema.org/resources/ontology/DCM](http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013-01-02&type=http%3A//dicom.nema.org/resources/ontology/DCM)\|110106

> The Audit Record Repository shall match this parameter with the AuditEvent.type field (DICOM EventID). </li>

<li> subtype is parameter of token type. This parameter identifies the specific IHE transaction that originates the audit record. The parameter value can contain the namespace URI urn:ihe:event-type-code to search for audit messages triggered by IHE transactions with the defined audit message. Each IHE transaction that defines an


> ATNA messages, specifies a code identifying the transaction itself, and assigns this code to the EventTypeCode element within the [ITI-20] audit record.
>
> For example, to search AuditEvent Resources related to [Retrieve Document Set [ITI-43]](https://profiles.ihe.net/ITI/TF/Volume2/ITI-43.html) transactions:
>
> [http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013-01-02&subtype=urn:ihe:event-type-code](http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013-01-02&subtype=urn%3Aihe%3Aevent-type-code)\|ITI-43
>
> The Audit Record Repository shall match this parameter with the AuditEvent.subtype
>
> field (DICOM EventTypeCode). </li>

<li> outcome is a parameter of token type. This parameter represents whether the event succeeded or failed. The parameter value shall contain the namespace URI <http://hl7.org/fhir/audit-event-outcome> and a code taken from the related value set. See [http://hl7.org/fhir/R4/valueset-audit-event-outcome.html.](http://hl7.org/fhir/R4/valueset-audit-event-outcome.html)


> To search AuditEvent Resources related to failed events:
>
> [http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013-01-02&outcome=http://hl7.org/fhir/audit-event-outcome](http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013-01-02&outcome=http%3A//hl7.org/fhir/audit-event-outcome)\|4,8,12
>
> The Audit Record Repository shall match this parameter with the AuditEvent.outcome
>
> field (DICOM EventOutcomeIndicator).</li>
>
> The HL7<sup>®</sup> FHIR<sup>®</sup> standard provides additional search parameters. This transaction does not define specific behavior on those parameters (such as \_sort, \_include, etc.). See [http://hl7.org/fhir/R4/search.html](http://hl7.org/fhir/R4/search.html) for details about available parameters.

###### 3.81.4.1.2.3 Populating Expected Response Format

> The HL7<sup>®</sup> FHIR<sup>®</sup> standard provides encodings for responses as either XML or JSON. The Audit Record Repository shall support both message encodings. The Audit Consumer shall support one and may optionally support both encodings. For Desired Response Encoding and format negotiation see ITI TF-2: Appendix Z.6.

##### 3.81.4.1.3 Expected Actions

> The Audit Record Repository (ARR) maintains a database of audit events. The Audit Record Repository retains data according to local policies, and some data may be deleted.
>
> The Audit Record Repository shall return all the audit events stored in its database that match the query parameters, and which the requester is authorized to view (see [ITI TF-1: 9.4](https://profiles.ihe.net/ITI/TF/Volume1/ch-9.html#9.4) for further details).
>
> When performing matching based on the search parameters, the Audit Record Repository shall:
<ul>
<li> Select all audit records that have a time interval specified in the request URL </li>

<li> If search parameters other than those defined in Section 3.81.4.1.2.2 (e.g., \_sort,

> \_include FHIR search result parameters) are specified in the request URL, then
<ul>
<li> If the Audit Record Repository does not support the parameter, it shall be ignored; </li>

<li> If the Audit Record Repository supports the parameter, the matching or other behavior shall comply with the matching rules for its datatype in FHIR </li>
</ul>
</ul>
> The Audit Record Repository shall return matching resources using the Retrieve ATNA Audit Event Response Message. See Section 3.81.4.2.

#### 3.81.4.2 Retrieve ATNA Audit Event Response Message

> The Audit Record Repository sends the Retrieve ATNA Audit Event Response message in response to a query from an Audit Consumer.

##### 3.81.4.2.1 Trigger Events

> The Audit Record Repository creates this message when it receives and processes a Retrieve ATNA Audit Event message.

##### 3.81.4.2.2 Message Semantics

> When the Audit Record Repository successfully processes the search request, it shall return the matching AuditEvent Resources inside a FHIR Bundle Resource.
>
> The “Content-Type” of the response will depend upon the response format negotiation described in ITI TF-2: Appendix Z.6.
>
> If the date search parameter is missing (see Section 3.81.4.1.2.1), the Audit Record Repository may return HTTP response code 400 - Bad Request.
>
> If the specified search parameters do not result in any matching audit record, the Audit Record Repository shall return HTTP response of success 200, with an empty FHIR bundle.
>
> If the requested data size is considered excessive by the Audit Record Repository, it may choose to return the results in a series of pages (see [https://www.hl7.org/fhir/R4/http.html#paging)](https://www.hl7.org/fhir/R4/http.html#paging).
>
> Other HTTP response codes may be returned by the Audit Record Repository, indicating conditions outside of the scope of this transaction, for example, 401 – Authentication Failed might be returned if Audit Record Repository is grouped with the Kerberized Server in the EUA Profile. See ITI TF-2: Appendix Z.7 “Guidance on Access Denied Results”.
>
> The Audit Record Repository should complement the returned error code with a human readable description of the error condition.
>
> Audit Record Repository may return HTTP redirect responses (responses with values of 301, 302, 303, or 307) in response to a request. Audit Consumers must follow redirects, but if a loop is detected, it may report an error.

###### 3.81.4.2.2.1  Mapping between FHIR and DICOM for query interaction

> The mapping rules between FHIR AuditEvent Resources and DICOM AuditMessage format is based on FHIR Table 6.4.7.4 [(http://hl7.org/fhir/R4/auditevent-mappings.html)](http://hl7.org/fhir/R4/auditevent-mappings.html) that is further constrained in Table 3.81.4.2.2.1-1.
>
> Table 3.81.4.2.2.1-1 is normative and defined a strict alignment between the AuditEvent Resource and the DICOM AuditMessage. However, Table 3.81.4.2.2.1-1 does not aim to resolve the dissonance between the FHIR AuditEvent Resource and the DICOM AuditMessage, but rather it ensures interoperability between these two data models.
>
> The Audit Record Repository shall encode all the data within the DICOM format of the AuditMessage into the AuditEvent Resource(s) sent in the Retrieve ATNA Audit Event Response message.
>
> **Table 3.81.4.2.2.1-1: DICOM Tag Mapping for query interaction**

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 66%" />
</colgroup>
<thead>
<tr class="header">
<th><blockquote>
<p><strong>AuditEvent Resource</strong></p>
</blockquote></th>
<th><strong>AuditMessage</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>type</td>
<td>EventIdentification.EventID</td>
</tr>
<tr class="even">
<td>subtype</td>
<td>EventIdentification.EventTypeCode</td>
</tr>
<tr class="odd">
<td>action</td>
<td>EventIdentification@EventActionCode</td>
</tr>
<tr class="even">
<td>period</td>
<td>NOT PRESENT</td>
</tr>
<tr class="odd">
<td>recorded</td>
<td>EventIdentification@EventDateTime</td>
</tr>
<tr class="even">
<td>outcome</td>
<td>EventIdentification@EventOutcomeIndicator</td>
</tr>
<tr class="odd">
<td>outcomeDesc</td>
<td>EventIdentification.EventOutcomeDescription</td>
</tr>
<tr class="even">
<td>purposeOfEvent</td>
<td>EventIdentification.purposeOfUse</td>
</tr>
<tr class="odd">
<td>agent</td>
<td>ActiveParticipant</td>
</tr>
<tr class="even">
<td>agent.type (Note 1)</td>
<td>ActiveParticipant.RoleIDCode</td>
</tr>
<tr class="odd">
<td>agent.role (Note 1)</td>
<td>ActiveParticipant.RoleIDCode</td>
</tr>
<tr class="even">
<td>agent.who</td>
<td>ActiveParticipant@UserId</td>
</tr>
<tr class="odd">
<td>agent.altId</td>
<td>ActiveParticipant@AlternativeUserId</td>
</tr>
<tr class="even">
<td>agent.name</td>
<td>ActiveParticipant@UserName</td>
</tr>
<tr class="odd">
<td>agent.requestor</td>
<td>ActiveParticipant@UserIsRequestor</td>
</tr>
<tr class="even">
<td>agent.location</td>
<td>NOT PRESENT</td>
</tr>
<tr class="odd">
<td>agent.policy</td>
<td>ParticipantRoleIDCode</td>
</tr>
<tr class="even">
<td>agent.media</td>
<td>ActiveParticipant.MediaIdentifier.MediaType</td>
</tr>
<tr class="odd">
<td>agent.network.address</td>
<td>ActiveParticipant@NetworkAccessPointID</td>
</tr>
<tr class="even">
<td>agent.network.type</td>
<td>ActiveParticipant@NetworkAccessPointTypeCode</td>
</tr>
<tr class="odd">
<td>agent.purposeOfUse</td>
<td>NOT PRESENT</td>
</tr>
<tr class="even">
<td>source</td>
<td>AuditSourceIdentification</td>
</tr>
<tr class="odd">
<td>source.site</td>
<td>AuditSourceIdentification@AuditEnterpriseSiteId</td>
</tr>
<tr class="even">
<td>source.observer</td>
<td>AuditSourceIdentification@AuditSourceId</td>
</tr>
<tr class="odd">
<td>source.type</td>
<td>AuditSourceIdentification.AuditSourcetypeCode</td>
</tr>
<tr class="even">
<td>entity</td>
<td>ParticipantObjectIdentification</td>
</tr>
<tr class="odd">
<td>entity.what</td>
<td>ParticipantObjectIdentification@ParticipantObjectID and ParticipantObjectIdentification.ParticipantObjectIDTypeCode</td>
</tr>
<tr class="even">
<td>entity.type</td>
<td>ParticipantObjectIdentification@ParticipantObjectTypeCode</td>
</tr>
<tr class="odd">
<td>entity.role</td>
<td>ParticipantObjectIdentification@ParticipantObjectTypeCodeRole</td>
</tr>
<tr class="even">
<td>entity.lifecycle</td>
<td>ParticipantObjectIdentification@ParticipantObjectDataLifeCycle</td>
</tr>
<tr class="odd">
<td>entity.securityLabel</td>
<td>ParticipantObjectIdentification@ParticipantObjectSensitivity</td>
</tr>
<tr class="even">
<td>entity.name</td>
<td>ParticipantObjectIdentification.ParticipantObjectName</td>
</tr>
<tr class="odd">
<td>entity.description</td>
<td>NOT PRESENT</td>
</tr>
<tr class="even">
<td>entity.query</td>
<td>ParticipantObjectIdentification.ParticipantObjectQuery</td>
</tr>
<tr class="odd">
<td>entity.detail</td>
<td>ParticipantObjectIdentification.ParticipantObjectDetail</td>
</tr>
<tr class="even">
<td>entity.detail.type</td>
<td>ParticipantObjectIdentification.ParticipantObjectDetail@type</td>
</tr>
<tr class="odd">
<td>entity.detail.ValueBase64Binary</td>
<td>ParticipantObjectIdentification.ParticipantObjectDetail@value</td>
</tr>
</tbody>
</table>

>
> Note 1: If the Audit Record Repository knows the ActiveParticipant.RoleIDCode as a type, it should be mapped to
>
> agent.type. Otherwise the default mapping is to agent.role.
>
> Note 2: Values recorded in the ParticipantObjectIdentification.ParticipantObjectDescription element shall be represented in the extension defined in [https://www.hl7.org/fhir/R4/auditevent-profiles.html - extensions](https://www.hl7.org/fhir/R4/auditevent-profiles.html#extensions) .
>
###### 3.81.4.2.2.2  FHIR Bundle of Audit Events Messages

> When the search is successful, the body of the Response message shall contain a FHIR Bundle of AuditEvent Resources.
>
> Example XML format:

##### 3.81.4.2.3 Expected Actions

> The Audit Consumer may further analyze the data received within the FHIR Bundle of AuditEvent Resources.

### 3.81.5 Security Considerations

> See the general Security Considerations in [ITI TF-1: 9.5.](https://profiles.ihe.net/ITI/TF/Volume1/ch-9.html#9.5)

#### 3.81.5.1 Security Audit Considerations

> This transaction may involve the disclosure of sensitive information. Logging these retrieval transactions as a query event is appropriate. However, ATNA Profile does not require the Audit Record Repository to be able to send audit records using the Record Audit Event [ITI-20] transaction. The Audit Record Repository shall create and store locally an audit event as follows:

<table>
<colgroup>
<col style="width: 15%" />
<col style="width: 29%" />
<col style="width: 7%" />
<col style="width: 47%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th><blockquote>
<p><strong>Field Name</strong></p>
</blockquote></th>
<th><strong>Opt</strong></th>
<th><blockquote>
<p><strong>Value Constraints</strong></p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td rowspan="3"><p><strong>Event</strong></p>
<blockquote>
<p>AuditMessage/ EventIdentification</p>
</blockquote></td>
<td><blockquote>
<p>EventID</p>
</blockquote></td>
<td>M</td>
<td>EV <a href="http://dicom.nema.org/medical/dicom/current/output/chtml/part16/chapter_D.html#DCM_110101">(110101, DCM, "Audit Log Used")</a></td>
</tr>
<tr class="even">
<td><blockquote>
<p>EventActionCode</p>
</blockquote></td>
<td>M</td>
<td>“R” (Read)</td>
</tr>
<tr class="odd">
<td><blockquote>
<p><em>EventDateTime</em></p>
</blockquote></td>
<td><em>U</em></td>
<td><em>not specialized</em></td>
</tr>
<tr class="header">
<th rowspan="2"></th>
<th><blockquote>
<p><em>EventOutcomeIndicator</em></p>
</blockquote></th>
<th><em>U</em></th>
<th><em>not specialized</em></th>
</tr>
<tr class="odd">
<th><blockquote>
<p>EventTypeCode</p>
</blockquote></th>
<th>M</th>
<th>EV(“ITI-81”, “IHE Transactions”, “Retrieve ATNA AuditEvent”)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td colspan="4">Source (Document Administrator) (1)</td>
</tr>
<tr class="even">
<td colspan="4">Human Requestor (0..1)</td>
</tr>
<tr class="odd">
<td colspan="4">Destination (Document Registry) (1)</td>
</tr>
<tr class="even">
<td colspan="4">Audit Source (Document Administrator) (1)</td>
</tr>
<tr class="odd">
<td colspan="4">AuditEvent Message (0..n)</td>
</tr>
</tbody>
</table>

> Where:

<table>
<colgroup>
<col style="width: 16%" />
<col style="width: 29%" />
<col style="width: 6%" />
<col style="width: 47%" />
</colgroup>
<thead>
<tr class="header">
<th><blockquote>
<p><strong>Source</strong></p>
</blockquote></th>
<th><em>UserID</em></th>
<th><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td rowspan="6"><blockquote>
<p>AuditMessage/ ActiveParticipant</p>
</blockquote></td>
<td>AlternativeUserID</td>
<td>M</td>
<td><blockquote>
<p>The process ID as used within the local operating system in the local system logs.</p>
</blockquote></td>
</tr>
<tr class="even">
<td><em>UserName</em></td>
<td><em>U</em></td>
<td><blockquote>
<p><em>not specialized</em></p>
</blockquote></td>
</tr>
<tr class="odd">
<td><em>UserIsRequestor</em></td>
<td><em>U</em></td>
<td><blockquote>
<p><em>not specialized</em></p>
</blockquote></td>
</tr>
<tr class="even">
<td>RoleIDCode</td>
<td>M</td>
<td><blockquote>
<p>EV(110153, DCM, “Source Role ID”)</p>
</blockquote></td>
</tr>
<tr class="odd">
<td>NetworkAccessPointTypeCode</td>
<td>M</td>
<td><blockquote>
<p>“1” for machine (DNS) name, “2” for IP address</p>
</blockquote></td>
</tr>
<tr class="even">
<td>NetworkAccessPointID</td>
<td>M</td>
<td><blockquote>
<p>The machine name or IP address.</p>
</blockquote></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 16%" />
<col style="width: 29%" />
<col style="width: 6%" />
<col style="width: 47%" />
</colgroup>
<thead>
<tr class="header">
<th rowspan="7"><blockquote>
<p><strong>Human Requestor (if known)</strong></p>
<p>AuditMessage/ ActiveParticipant</p>
</blockquote></th>
<th>UserID</th>
<th>M</th>
<th><blockquote>
<p>Identity of the human that initiated the transaction.</p>
</blockquote></th>
</tr>
<tr class="odd">
<th><em>AlternativeUserID</em></th>
<th><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr class="header">
<th><em>UserName</em></th>
<th><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr class="odd">
<th><em>UserIsRequestor</em></th>
<th><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr class="header">
<th>RoleIDCode</th>
<th>M</th>
<th><blockquote>
<p>Access Control role(s) the user holds that allows this transaction.</p>
</blockquote></th>
</tr>
<tr class="odd">
<th><em>NetworkAccessPointTypeCode</em></th>
<th><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr class="header">
<th><em>NetworkAccessPointID</em></th>
<th><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 16%" />
<col style="width: 29%" />
<col style="width: 6%" />
<col style="width: 47%" />
</colgroup>
<thead>
<tr class="header">
<th><blockquote>
<p><strong>Destination</strong></p>
</blockquote></th>
<th>UserID</th>
<th>M</th>
<th><blockquote>
<p>SOAP endpoint URI.</p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td rowspan="6"><blockquote>
<p>AuditMessage/ ActiveParticipant</p>
</blockquote></td>
<td><em>AlternativeUserID</em></td>
<td><em>U</em></td>
<td><blockquote>
<p><em>not specialized</em></p>
</blockquote></td>
</tr>
<tr class="even">
<td><em>UserName</em></td>
<td><em>U</em></td>
<td><blockquote>
<p><em>not specialized</em></p>
</blockquote></td>
</tr>
<tr class="odd">
<td><em>UserIsRequestor</em></td>
<td><em>U</em></td>
<td><blockquote>
<p><em>not specialized</em></p>
</blockquote></td>
</tr>
<tr class="even">
<td>RoleIDCode</td>
<td>M</td>
<td><blockquote>
<p>EV(110152, DCM, “Destination Role ID”)</p>
</blockquote></td>
</tr>
<tr class="odd">
<td>NetworkAccessPointTypeCode</td>
<td>M</td>
<td><blockquote>
<p>“1” for machine (DNS) name, “2” for IP address</p>
</blockquote></td>
</tr>
<tr class="even">
<td>NetworkAccessPointID</td>
<td>M</td>
<td><blockquote>
<p>The machine name or IP address.</p>
</blockquote></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 16%" />
<col style="width: 29%" />
<col style="width: 6%" />
<col style="width: 47%" />
</colgroup>
<thead>
<tr class="header">
<th rowspan="3"><blockquote>
<p><strong>Audit Source</strong></p>
</blockquote>
<p>AuditMessage/AuditSou rceIdentification</p></th>
<th><em>AuditSourceID</em></th>
<th><em>U</em></th>
<th><em>not specialized</em></th>
</tr>
<tr class="odd">
<th><em>AuditEnterpriseSiteID</em></th>
<th><em>U</em></th>
<th><em>not specialized</em></th>
</tr>
<tr class="header">
<th><em>AuditSourceTypeCode</em></th>
<th><em>U</em></th>
<th><em>not specialized</em></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 16%" />
<col style="width: 29%" />
<col style="width: 6%" />
<col style="width: 47%" />
</colgroup>
<thead>
<tr class="header">
<th rowspan="9"><blockquote>
<p><strong>AuditEvent Message</strong></p>
<p>AuditMessage/ ParticipantObjectIdentif ication</p>
</blockquote></th>
<th>ParticipantObjectTypeCode</th>
<th>M</th>
<th><blockquote>
<p>“2” (System object)</p>
</blockquote></th>
</tr>
<tr class="odd">
<th>ParticipantObjectTypeCodeRole</th>
<th>M</th>
<th><blockquote>
<p>“13” (Security Resource)</p>
</blockquote></th>
</tr>
<tr class="header">
<th><em>ParticipantObjectDataLifeCycle</em></th>
<th><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr class="odd">
<th>ParticipantObjectIDTypeCode</th>
<th>M</th>
<th><blockquote>
<p>EV(“12”, “RFC-3881”, "URI")</p>
</blockquote></th>
</tr>
<tr class="header">
<th><em>ParticipantObjectSensitivity</em></th>
<th><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr class="odd">
<th>ParticipantObjectID</th>
<th>M</th>
<th><blockquote>
<p>The URI of the Audit log</p>
</blockquote></th>
</tr>
<tr class="header">
<th>ParticipantObjectName</th>
<th>U</th>
<th><blockquote>
<p>“Security Audit Log”</p>
</blockquote></th>
</tr>
<tr class="odd">
<th><em>ParticipantObjectQuery</em></th>
<th><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr class="header">
<th><em>ParticipantObjectDetail</em></th>
<th><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
</thead>
<tbody>
</tbody>
</table>
