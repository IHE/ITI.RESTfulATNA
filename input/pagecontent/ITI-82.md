## 3.82 Retrieve Syslog Event [ITI-82]

> This transaction supports the retrieval of syslog messages from the Audit Record Repository subject to parameters that limit the retrieval.

### Scope

> The Retrieve Syslog Event transaction is used to search events recorded.

### Use-case Roles

> **Actor:** Audit Record Repository
>
> **Role:** Provides storage for syslog messages, and responds to queries for a portion of the stored messages.
>
> **Actor:** Audit Consumer
>
> **Role:** Queries for audit records.

### Referenced Standards

> RFC2616 IETF Hypertext Transfer Protocol – HTTP/1.1
>
> RFC4627 The application/json Media Type for JavaScript Object Notation (JSON)

> RFC6585 IETF Additional HTTP Status Codes RFC5424 The Syslog Protocol
>
> RFC3339 Date and Time on the Internet: Timestamps

### Messages

### 

> Audit Consumer Audit Record Repository
>
> **Figure 3.82.4-1: Interaction Diagram**

###  Retrieve Syslog Event Request Message

> This message shall be an HTTP GET parameterized search from an Audit Consumer to an Audit Record Repository. The Audit Record Repository maintains a database of received syslog messages. This database may be a subset of all messages received and it may include messages that do not adhere to the IHE Audit Trail format defined in the Record Audit Event [ITI-20] transaction. See [ITI TF-2: 3.20.7](https://profiles.ihe.net/ITI/TF/Volume2/ITI-20.html#3.20.7) Audit Message Format. The Audit Record Repository may have selection criteria for what kinds of messages are kept for later search, how long different kinds of messages are kept, etc.

### Trigger Events

> This message is sent when the Audit Consumer needs syslog messages to process.

### Message Semantics

> The Retrieve Syslog Event Request message is an HTTP GET request sent by the Audit Consumer to the Retrieve Syslog Event URL on the Audit Record Repository. The “search” target is formatted as:
>
> \<scheme\>://\<authority\>/\<path\>/syslogsearch?date=le[start-time]&date=ge[stop-time]&\<query\>
>
> Where:

- \<scheme\> shall be either http or https. The use of http or https is a policy decision, but https is usually appropriate due to confidentiality of syslog message content;


- \<authority\> shall be represented as a host (either IP address or DNS name) followed optionally by a colon and port number.

- The Audit Record Repository may use \<path\> to segregate the search from other services.

- “syslogsearch” is a required part of the URL that allows the Audit Consumer to ask for syslog messages stored in the Audit Record Repository.

- At least one date search parameters id required. See Section 3.82.4.1.2.1.

- **“&”** is a conditional parameter that shall be present if the \<query\> parameter is present.

- \<query\>, if present, represents additional search parameters. See Section 3.82.4.1.2.2.

> The Audit Consumer may indicate the preferred format of the response in the HTTP “Accept” header.

### Date Search Parameters

> One or two **date** parameters shall be present in every search by the Audit Consumer and shall be supported by the Audit Record Repository. Using two parameters allows the Audit Consumer to specify the time frame of creation of syslog messages of interest and enable the Audit Consumer to constrain the number of syslog messages returned. The lower and upper bound for time shall be in RFC3339 format.
>
> Note: RFC3339 format is the format mandated by Syslog for time stamps and is a sub-set of the XML date-time data format.
>
> To search syslog messages created during the whole day of January 5, 2013, the search URL is:
>
> <http://example.com/ARRservice/syslogsearch?date=ge2013-01-05&date=le2013-01->05
>
> This parameter matches with the time of the syslog message creation.

### Additional Search Parameters

> The search parameters in this section may be supported by the Audit Consumer and shall be supported by the Audit Record Repository. These parameters can be used by the Audit Consumer to refine search requests.
>
> The Audit Consumer may include additional search parameters. These search parameters shall be encoded in accordance with RFC3986 for encoding GET queries.
>
> The search string is encoded as a list of search parameter/value pairs, using the parameter names in column 2 of Table 3.82.4.1.2.2-1 to indicate the syslog message element being matched. There is a search parameter assigned for each syslog metadata element. In all cases:

- The search values shall be encoded as strings.

- The syslog message is considered to match if the value string is a sub-string found in the specified message element.


> **Table 3.82.4.1.2.2-1: Retrieve Syslog Event search parameters mapping with syslog metadata**

<table>
<colgroup>
<col style="width: 48%" />
<col style="width: 51%" />
</colgroup>
<thead>
<tr class="header">
<th><blockquote>
<p><strong>Syslog RFC5424 element</strong></p>
</blockquote></th>
<th><blockquote>
<p><strong>Retrieve Syslog Event Search Parameter</strong></p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PRI</td>
<td>pri</td>
</tr>
<tr class="even">
<td>VERSION</td>
<td>version</td>
</tr>
<tr class="odd">
<td>HOSTNAME</td>
<td>hostname</td>
</tr>
<tr class="even">
<td>APP-NAME</td>
<td>app-name</td>
</tr>
<tr class="odd">
<td>PROCID</td>
<td>procid</td>
</tr>
<tr class="even">
<td>MSG-ID</td>
<td>msg-id</td>
</tr>
<tr class="odd">
<td>MSG</td>
<td>msg</td>
</tr>
</tbody>
</table>

> HTTP allows for multiple instances of a parameter to be requested with different values. Multiple values of the same parameter name shall be treated as an OR relationship for string matches. The Audit Consumer may combine different search parameters. The matching of different search parameters is combined with an AND relationship. Some examples of how this works are:

- To search for “hostname=Frodo” and “hostname=Bilbo” will return the combination of all event reports from either host Frodo or Bilbo during the time interval:

> <http://example.com/ARRservice/syslogsearch?date=ge2013-01-01&date=le2013-01-02&hostname=Frodo&hostname=Bilbo>

- To search for “hostname=Frodo” and “proc-id=system” means all events from the host “Frodo” with proc-id of “system” during the time interval:

> <http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013-01-02&hostname=Frodo&proc-id=system>

- To search for “hostname=Frodo”, “hostname=Bilbo”, and “proc-id=system” will return the combination of all event reports from either host Frodo or Bilbo that have the proc-id of “system” during the time interval:

> <http://example.com/ARRservice/syslogsearch?date=ge2013-01-01&date=le2013-01-02&hostname=Frodo&hostname=Bilbo>
>
> This form of search is not a substitute for additional processing by the Audit Consumer. The Audit Record Repository can return a large quantity of syslog messages. The Audit Consumer may need to perform further processing to select the information needed for a report.
>
> The Audit Record Repository shall document in its IHE Integration Statement any additional parameters supported.

###  Expected Actions

> The Audit Record Repository maintains a database of syslog messages. The Audit Record Repository shall return all the syslog messages stored in that database that match the query parameters, and which the requester is authorized to view (see [ITI TF-1: 9.4](https://profiles.ihe.net/ITI/TF/Volume1/ch-9.html#9.4) for further details). The Audit Record Repository retains data in accordance to local policies and some data may be deleted.
>
> The Audit Record Repository shall respond with a Syslog Event Response message described in Section 3.82.4.2.
>
> When performing matching based on the search parameters, the Audit Record Repository shall:

- Select all messages that have a time interval specified in the request URL.

- If search parameters other than those defined in Section 3.82.4.1.2.2 are specified in the request URL, then if the parameter is not supported, it shall be ignored; otherwise, if this parameter is supported, the Audit Record Repository shall apply matching criteria in accordance to that.

- Select a response format following the rules of RFC7231 Section 5.3.2. The Audit Record Repository shall support JSON format (i.e., application/json). In the absence of an Accept preference, JSON shall be used.

### Syslog Event Response Message

> The Audit Record Repository sends the Syslog Event Response message in response to a query from an Audit Consumer

### Trigger Events

> The Audit Record Repository creates this message when it receives and processes a Retrieve Syslog Event Request message.

### Message Semantics

> The Content-Length entity-header field shall be returned, unless this is prohibited by the rules in RFC2616 Section 4.4, or subsequent versions of the HTTP specification.
>
> Note: RFC2616 specifies that this field *should* be returned. This transaction strengthens that requirement.
>
> In case of success, the Audit Record Repository shall return the syslog messages that match the search parameters, encoded as an array of messages encoded in one of the formats specified in the Accept header of the request message. The Syslog Event Response message shall carry a HTTP response status code of 200, and its body shall contain an Array of syslog messages in the selected format.
>
> Each syslog message shall be encoded as described in Table 3.38.4.2.2-1:
>
> **Table 3.82.4.2.2-1: Syslog Message Encoding**

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 32%" />
</colgroup>
<thead>
<tr class="header">
<th><blockquote>
<p><strong>Syslog Metadata</strong></p>
</blockquote></th>
<th><blockquote>
<p><strong>JSON element</strong></p>
</blockquote></th>
<th><blockquote>
<p><strong>dataType</strong></p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PRI</td>
<td>Pri</td>
<td>&lt;<a href="http://hl7.org/fhir/2015May/datatypes.html#string">string</a>&gt;</td>
</tr>
<tr class="even">
<td>VERSION</td>
<td>Version</td>
<td>&lt;<a href="http://hl7.org/fhir/2015May/datatypes.html#string">string</a>&gt;</td>
</tr>
<tr class="odd">
<td>TIMESTAMP</td>
<td>Timestamp</td>
<td>see RFC5424 (Sec. 6.2.3)</td>
</tr>
<tr class="even">
<td>HOSTNAME</td>
<td>Hostname</td>
<td>&lt;<a href="http://hl7.org/fhir/2015May/datatypes.html#string">string</a>&gt;</td>
</tr>
<tr class="odd">
<td>APP-NAME</td>
<td>App-name</td>
<td>&lt;<a href="http://hl7.org/fhir/2015May/datatypes.html#string">string</a>&gt;</td>
</tr>
<tr class="even">
<td>PROCID</td>
<td>Procid</td>
<td>&lt;<a href="http://hl7.org/fhir/2015May/datatypes.html#string">string</a>&gt;</td>
</tr>
<tr class="odd">
<td>MSG-ID</td>
<td>Msg-id</td>
<td>&lt;<a href="http://hl7.org/fhir/2015May/datatypes.html#string">string</a>&gt;</td>
</tr>
<tr class="even">
<td>MSG</td>
<td>Msg</td>
<td>&lt;<a href="http://hl7.org/fhir/2015May/datatypes.html#string">string</a>&gt;</td>
</tr>
<tr class="odd">
<td>STRUCTURED_DATA</td>
<td>Structured_data</td>
<td>&lt;<a href="http://hl7.org/fhir/2015May/datatypes.html#string">string</a>&gt;</td>
</tr>
</tbody>
</table>


> If the date parameter is missing, the Audit Record Repository may return HTTP response code 400 - Bad Request.
>
> If the specified parameters do not result in any matching syslog messages, the Audit Record Repository shall report a Response of Success (HTTP 200) with an empty JSON array.
>
> If the requested data size is excessive, the Audit Record Repository may respond with HTTP 206 Partial Content. If the response is 206 Partial Content, then the response body may contain a subset of the syslog messages that match the search. This transaction does not define query result pagination mechanisms, so the Audit Consumer cannot query for remaining content in case of http 206 error received.
>
> If the “Accept” header provided in the Request is not supported by the Audit Record Repository, it may send a 415 “Unsupported Media Type” error.
>
> Note: Other HTTP response codes may be returned by the Audit Record Repository, indicating conditions outside of the scope of this transaction, for example, 401 – Authentication Failed might be returned if Audit Record Repository also supports the IUA Profile and is given an expired authorization token or is grouped with the EUA Profile Kerberized Server.
>
> The Audit Record Repository should complement the returned error code with a human readable description of the error condition.
>
> Audit Record Repository may return HTTP redirect responses (responses with values of 301, 302, 303, or 307) in response to a request. Audit Consumers must follow redirects, but if a loop is detected, it may report an error.

### JSON encoded array of Syslog Messages

> The Audit Record Repository shall construct a JSON array of syslog messages by parsing the message elements in each matching Syslog as defined in RFC5424 as strings identified by the element name in RFC5424. If an element is absent from the syslog message, the Audit Record Repository shall not include this element in the JSON encoding.
>
<table>
<colgroup>
<col style="width: 24%" />
<col style="width: 75%" />
</colgroup>
<thead>
<tr class="header">
<th rowspan="3"></th>
<th><p>[</p>
<blockquote>
<p>{</p>
</blockquote></th>
</tr>
<tr class="odd">
<th><blockquote>
<p>"Pri": "string",</p>
</blockquote></th>
</tr>
<tr class="header">
<th><blockquote>
<p>"Version": "string",</p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1360</td>
<td><blockquote>
<p>"Timestamp": "2015-03-17T00:05",</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
<td><blockquote>
<p>"Hostname": "string",</p>
</blockquote></td>
</tr>
<tr class="odd">
<td></td>
<td><blockquote>
<p>"App-name": "string",</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
<td><blockquote>
<p>"Procid": "string",</p>
</blockquote></td>
</tr>
<tr class="odd">
<td></td>
<td><blockquote>
<p>"Msg-id": "string",</p>
</blockquote></td>
</tr>
<tr class="even">
<td>1365</td>
<td><blockquote>
<p>"Msg": "string1",</p>
</blockquote></td>
</tr>
<tr class="odd">
<td></td>
<td><blockquote>
<p>"Structured_data": "string"</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
<td><blockquote>
<p>},</p>
</blockquote></td>
</tr>
<tr class="odd">
<td></td>
<td><blockquote>
<p>{</p>
</blockquote></td>
</tr>
<tr class="even">
<td>1370</td>
<td><blockquote>
<p>"Pri": "string",</p>
<p>"Version": "string",</p>
</blockquote></td>
</tr>
<tr class="odd">
<td></td>
<td><blockquote>
<p>"Timestamp": "2015-03-17T00:05",</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
<td><blockquote>
<p>"Hostname": "string",</p>
</blockquote></td>
</tr>
<tr class="odd">
<td></td>
<td><blockquote>
<p>"App-name": "string",</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
<td><blockquote>
<p>"Procid": "string",</p>
</blockquote></td>
</tr>
<tr class="odd">
<td>1375</td>
<td><blockquote>
<p>"Msg-id": "string",</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
<td><blockquote>
<p>"Msg": "string2"</p>
</blockquote></td>
</tr>
<tr class="odd">
<td></td>
<td><blockquote>
<p>},</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
<td><blockquote>
<p>{</p>
</blockquote></td>
</tr>
<tr class="odd">
<td></td>
<td><blockquote>
<p>"Pri": "string",</p>
</blockquote></td>
</tr>
<tr class="even">
<td>1380</td>
<td><blockquote>
<p>"version": "string",</p>
</blockquote></td>
</tr>
<tr class="odd">
<td></td>
<td><blockquote>
<p>"Timestamp": "2015-03-17T00:05",</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
<td><blockquote>
<p>"Hostname": "string",</p>
</blockquote></td>
</tr>
<tr class="odd">
<td></td>
<td><blockquote>
<p>"App-name": "string",</p>
</blockquote></td>
</tr>
<tr class="even">
<td>1385</td>
<td><blockquote>
<p>"Procid": "string",</p>
<p>"Msg-id": "string",</p>
</blockquote></td>
</tr>
<tr class="odd">
<td></td>
<td><blockquote>
<p>"Msg": "string3"</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
<td><blockquote>
<p>}</p>
</blockquote>
<p>]</p></td>
</tr>
</tbody>
</table>

> **Figure 3.82.4.2.2.1-1: Example JSON encoded array of syslog messages**

###  Expected Actions

> The Audit Consumer shall process the response according to the capabilities of its application. The processing is not constrained by IHE.
>
> The Audit Record Repository shall create and store locally an audit event structured in accordance to requirements defined in DICOM PS3.15 Section A.5.3.2 “Audit Log Used”.

### Security Considerations

> See the general Security Considerations in [ITI TF-1: 9.5.](https://profiles.ihe.net/ITI/TF/Volume1/ch-9.html#9.5)

### Security Audit Considerations

> This transaction may involve the disclosure of sensitive information. Logging these retrieval transactions as a query event is appropriate. However, ATNA Profile does not require the Audit

> Record Repository to be able to send audit records using the Record Audit Event [ITI-20] transaction. The Audit Record Repository shall create and store locally an audit event as follows:

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
<td rowspan="5"><p><strong>Event</strong></p>
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
<tr class="even">
<td><blockquote>
<p><em>EventOutcomeIndicator</em></p>
</blockquote></td>
<td><em>U</em></td>
<td><em>not specialized</em></td>
</tr>
<tr class="odd">
<td><blockquote>
<p>EventTypeCode</p>
</blockquote></td>
<td>M</td>
<td>EV(“ITI-82”, “IHE Transactions”, “Retrieve Syslog Event”)</td>
</tr>
<tr class="even">
<td colspan="4">Source (Audit Consumer) (1)</td>
</tr>
<tr class="odd">
<td colspan="4">Human Requestor (0..1)</td>
</tr>
<tr class="even">
<td colspan="4">Destination (Audit Record Repository) (1)</td>
</tr>
<tr class="odd">
<td colspan="4">Audit Source (Audit Record Repository) (1)</td>
</tr>
<tr class="even">
<td colspan="4">Syslog message (0,..n)</td>
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
<td rowspan="2"><blockquote>
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
<th rowspan="4"></th>
<th><em>UserIsRequestor</em></th>
<th><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr class="odd">
<th>RoleIDCode</th>
<th>M</th>
<th><blockquote>
<p>EV(110152, DCM, “Destination Role ID”)</p>
</blockquote></th>
</tr>
<tr class="header">
<th>NetworkAccessPointTypeCode</th>
<th>M</th>
<th><blockquote>
<p>“1” for machine (DNS) name, “2” for IP address</p>
</blockquote></th>
</tr>
<tr class="odd">
<th>NetworkAccessPointID</th>
<th>M</th>
<th><blockquote>
<p>The machine name or IP address.</p>
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
<p><strong>Syslog message</strong></p>
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
