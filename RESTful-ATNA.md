## Integrating the Healthcare Enterprise

<img src="./media/image1.jpeg"
style="width:1.78905in;height:0.91667in" />

<table style="width:97%;">
<colgroup>
<col style="width: 5%" />
<col style="width: 11%" />
<col style="width: 80%" />
</colgroup>
<thead>
<tr>
<th style="text-align: center;">5</th>
<th></th>
<th style="text-align: center;"><p><strong>IHE IT
Infrastructure</strong></p>
<p><strong>Technical Framework Supplement</strong></p></th>
</tr>
</thead>
<tbody>
<tr>
<td>10</td>
<td></td>
<td><strong>Add RESTful ATNA (Query and Feed)</strong></td>
</tr>
<tr>
<td></td>
<td></td>
<td><p>HL7<sup>®</sup> FHIR<sup>®</sup> Release 4</p>
<p>Using Resources at FMM Level 3 and Normative</p></td>
</tr>
<tr>
<td style="text-align: center;">15</td>
<td></td>
<td style="text-align: center;"><strong>Rev. 3.6 – Trial
Implementation</strong></td>
</tr>
<tr>
<td>20</td>
<td><blockquote>
<p>Date: Author: Email:</p>
</blockquote></td>
<td><blockquote>
<p>November 25, 2025</p>
<p>IHE ITI Technical Committee <a
href="mailto:iti@ihe.net">iti@ihe.net</a></p>
</blockquote></td>
</tr>
</tbody>
</table>

> **Please verify you have the most recent version of this document.**
> See [<u>here</u>](https://profiles.ihe.net/ITI/index.html) for Trial
> Implementation and Final Text versions and
> [<u>here</u>](https://profiles.ihe.net/ITI/index.html#1.3) for Public
> Comment versions.
>
> Copyright © 2025: IHE International, Inc.

## Foreword

> This is a supplement to the IHE IT Infrastructure Technical Framework
> V20. Each supplement
>
> 30 undergoes a process of public comment and trial implementation
> before being incorporated into the volumes of the Technical
> Frameworks.
>
> This supplement is published on November 25, 2025 for trial
> implementation and may be available for testing at subsequent IHE
> Connectathons. The supplement may be amended based on the results of
> testing. Following successful testing it will be incorporated into the
> IT
>
> 35 Infrastructure Technical Framework. Comments are invited and may be
> submitted at
> [<u>http://www.ihe.net/ITI_Public_Comments</u>](http://www.ihe.net/ITI_Public_Comments/).
>
> This supplement describes changes to the existing technical framework
> documents.
>
> “Boxed” instructions like the sample below indicate to the Volume
> Editor how to integrate the relevant section(s) into the relevant
> Technical Framework volume.
>
> *Amend Section X.X by the following:*
>
> Where the amendment adds text, make the added text **<u>bold
> underline</u>**. Where the amendment removes text, make the removed
> text **~~bold strikethrough~~**. When entire new sections are added,
> introduce with editor’s instructions to “add new text” or similar,
> which for readability are not bolded or underlined.
>
> 45
>
> General information about IHE can be found at
> [<u>IHE.net</u>.](http://ihe.net/)
>
> Information about the IHE IT Infrastructure domain can be found at
> [<u>IHE Domains</u>](http://ihe.net/IHE_Domains/).
>
> Information about the organization of IHE Technical Frameworks and
> Supplements and the process used to create them can be found at
> [<u>Profiles</u>](http://ihe.net/Profiles/) and [<u>IHE
> Process</u>](http://ihe.net/IHE_Process/).
>
> 50 The current version of the IHE IT Infrastructure Technical
> Framework can be found at
> [<u>https://profiles.ihe.net/ITI/index.html</u>.](https://profiles.ihe.net/ITI/index.html)

### CONTENTS

> 55
>
> [Introduction to this Supplement 6](#introduction-to-this-supplement)
>
> [Open Issues and Questions 6](#open-issues-and-questions)
>
> [Closed Issues 7](#closed-issues)
>
> [IHE Technical Frameworks General Introduction
> 14](#ihe-technical-frameworks-general-introduction)
>
> 60 [9 Copyright Licenses 14](#copyright-licenses)
>
> [10 Trademark 14](#trademark)
>
> [IHE Technical Frameworks General Introduction Appendices
> 15](#ihe-technical-frameworks-general-introduction-appendices)
>
> [Appendix A – Actors 15](#appendix-a-actors)
>
> [Appendix B – Transactions 15](#appendix-b-transactions)
>
> 65 [Appendix D – Glossary 16](#appendix-d-glossary)
>
> [**Volume 1 – Profiles 17**](#volume-1-profiles)
>
> [9 Audit Trail and Node Authentication (ATNA)
> 17](#audit-trail-and-node-authentication-atna)

3.  [Audit Record Repository 19](#audit-record-repository)

> [9.1.1.5 Audit Consumer 19](#audit-consumer)
>
> 70 [9.2 ATNA Actor Options 20](#atna-actor-options)

3.  [Retrieve Audit Message Option 21](#retrieve-audit-message-option)

4.  [Retrieve Syslog Message Option 21](#retrieve-syslog-message-option)

<!-- -->

7.  [Audit Transport (ATX) Options 21](#audit-transport-atx-options)

    1.  [ATX: FHIR Feed Option 21](#_bookmark18)

> 75 [9.2.7.2 ATX: TLS Syslog Option 22](#_bookmark19)

2.  [Use Cases 22](#use-cases)

    4.  [Clinician Personal History of Study views process flow
        22](#clinician-personal-history-of-study-views-process-flow)

        1.  [Clinician Personal History of Study views use-case
            22](#clinician-personal-history-of-study-views-use-case)

    5.  [Patient access to his audit records process flow
        23](#patient-access-to-his-audit-records-process-flow)

> 80 [9.4.2.5.1 Patient access to his audit records use case
> 24](#patient-access-to-his-audit-records-use-case)

3.  [Technical Approach to Query use cases
    25](#technical-approach-to-query-use-cases)

> [9.5 ATNA Security Considerations 26](#atna-security-considerations)
>
> [**Volume 2 – Transactions 28**](#volume-2-transactions)
>
> [3.20 Record Audit Event \[ITI-20\] 28](#record-audit-event-iti-20)
>
> 85 [3.20.3 Referenced Standards 28](#_bookmark29)

4.  [Messages 29](#messages)

<!-- -->

4.  [Messages 30](#messages-1)

    2.  [Send Audit Resource Request Message – FHIR Feed Interaction
        30](#_bookmark32)

        1.  [Trigger Events 30](#trigger-events)

> 90 [3.20.4.2.2 Message Semantics 31](#message-semantics)

1.  [Mapping between DICOM Audit Message definitions and
    FHIR](#mapping-between-dicom-audit-message-definitions-and-fhir-auditevent-resource-for-the-fhir-feed-interactions)
    [AuditEvent Resource for the FHIR Feed interactions
    31](#mapping-between-dicom-audit-message-definitions-and-fhir-auditevent-resource-for-the-fhir-feed-interactions)

<!-- -->

3.  [Expected Actions 32](#expected-actions)

<!-- -->

3.  [Send Audit Resource Response 33](#_bookmark37)

> 95 [3.20.4.3.1 Trigger Events 33](#trigger-events-1)

2.  [Message Semantics 33](#_bookmark39)

> 100
>
> 105
>
> 110
>
> 115
>
> 120
>
> 125
>
> 130
>
> 135
>
> 140

3.  [Expected Actions 34](#expected-actions-1)

<!-- -->

4.  [Send Audit Bundle Request Message – FHIR Feed Interaction
    34](#_bookmark41)

    1.  [Trigger Events 34](#_bookmark42)

    2.  [Message Semantics 34](#_bookmark43)

    3.  [Expected Actions 35](#expected-actions-2)

5.  [Send Audit Bundle Response 36](#send-audit-bundle-response)

    1.  [Trigger Events 36](#trigger-events-3)

    2.  [Message Semantics 36](#_bookmark47)

    3.  [Expected Actions 37](#expected-actions-3)

<!-- -->

5.  [Security Considerations 37](#security-considerations)

<!-- -->

81. [Retrieve ATNA Audit Event \[ITI-81\]
    37](#retrieve-atna-audit-event-iti-81)

    1.  [Scope 38](#scope)

    2.  [Actor Roles 38](#actor-roles)

    3.  [Referenced Standards 38](#referenced-standards-1)

    4.  [Messages 38](#_bookmark54)

        1.  [Retrieve ATNA Audit Events Message
            39](#retrieve-atna-audit-events-message)

            1.  [Trigger Events 39](#trigger-events-4)

            2.  [Message Semantics 39](#_bookmark57)

                1.  [Date Search Parameters 39](#_bookmark58)

                2.  [Additional ATNA Search Parameters 40](#_bookmark59)

                3.  [Populating Expected Response Format
                    43](#populating-expected-response-format)

            3.  [Expected Actions 43](#expected-actions-4)

        2.  [Retrieve ATNA Audit Event Response Message
            44](#_bookmark62)

            1.  [Trigger Events 44](#trigger-events-5)

            2.  [Message Semantics 44](#_bookmark64)

                1.  [Mapping between FHIR and DICOM for query
                    interaction
                    45](#mapping-between-fhir-and-dicom-for-query-interaction)

                2.  [FHIR Bundle of Audit Events Messages
                    46](#fhir-bundle-of-audit-events-messages)

            3.  [Expected Actions 47](#expected-actions-5)

    5.  [Security Considerations 47](#security-considerations-1)

        1.  [Security Audit Considerations 47](#_bookmark69)

82. [Retrieve Syslog Event 49](#retrieve-syslog-event)

    1.  [Scope 49](#scope-1)

    2.  [Use-case Roles 49](#use-case-roles)

    3.  [Referenced Standards 49](#_bookmark73)

    4.  [Messages 50](#messages-2)

        1.  [Retrieve Syslog Event Request Message
            50](#retrieve-syslog-event-request-message)

            1.  [Trigger Events 50](#trigger-events-6)

            2.  [Message Semantics 50](#_bookmark77)

                1.  [Date Search Parameters
                    51](#date-search-parameters-1)

                2.  [Additional Search Parameters
                    51](#additional-search-parameters)

            3.  [Expected Actions 53](#expected-actions-6)

        2.  [Syslog Event Response Message
            53](#syslog-event-response-message)

            1.  [Trigger Events 53](#trigger-events-7)

            2.  [Message Semantics 53](#_bookmark83)

                1.  [JSON encoded array of Syslog Messages
                    54](#_bookmark84)

            3.  [Expected Actions 55](#expected-actions-7)

    5.  [Security Considerations 55](#security-considerations-2)

        1.  [Security Audit Considerations 55](#_bookmark87)

> 145 [Z.8 Mobile Security Considerations
> 57](#z.8-mobile-security-considerations)

## Introduction to this Supplement

> Whenever possible, IHE profiles are based on established and stable
> underlying standards. However, if an IHE domain determines that an
> emerging standard has high likelihood of industry adoption, and the
> standard offers significant benefits for the use cases it is
> attempting to address, the domain may develop IHE profiles based on
> such a standard. During Trial Implementation, the IHE domain will
> update and republish the IHE profile as the underlying standard
> evolves.
>
> Product implementations and site deployments may need to be updated in
> order for them to remain interoperable and conformant with an updated
> IHE profile.
>
> This Technical Framework Supplement incorporates content from Release
> 4 of the HL7<sup>®</sup> FHIR<sup>®</sup> standard. HL7 describes FHIR
> Change Management and Versioning at
> [<u>https://www.hl7.org/fhir/versions.html</u>](https://www.hl7.org/fhir/versions.html).
>
> HL7 provides a rating of the maturity of FHIR content based on the
> FHIR Maturity Model (FMM): level 0 (draft) through N (Normative). See
> [<u>http://hl7.org/fhir/versions.html#maturity</u>](http://hl7.org/fhir/versions.html#maturity).
>
> The FMM levels for FHIR content used in this supplement are:

<table style="width:45%;">
<colgroup>
<col style="width: 28%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr>
<th><blockquote>
<p><strong>FHIR Resource Name</strong></p>
</blockquote></th>
<th style="text-align: center;"><strong>FMM Level</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>Bundle</td>
<td style="text-align: center;">N</td>
</tr>
<tr>
<td>AuditEvent</td>
<td style="text-align: center;">3</td>
</tr>
<tr>
<td>OperationOutcome</td>
<td style="text-align: center;">N</td>
</tr>
</tbody>
</table>

> 150
>
> 155
>
> 160
>
> This supplement extends the functionalities of the ATNA Profile by
> introducing RESTful operations that could be used to submit and
> retrieve audit records. This allows light weight applications to
> easily manage the creation and the access audit information. This
> supplement is based on FHIR protocol and uses FHIR AuditEvent
> Resources in order to exchange audit records content. This supplement
> also defines a query transaction that enables access to raw syslog
> messages.

## Open Issues and Questions

1.  Should there be retrieve methods to get “most recent N events”? This
    would be a non-deterministic and constantly varying response in most
    cases.

2.  For ITI-82, the start-time and stop-time in \<date\> search
    parameters shall be in RFC3339 format. Do we need to further
    constrain the format of this parameter? Is this precise

> 165
>
> 170
>
> 175
>
> 180
>
> 185
>
> 190
>
> 195
>
> enough? Doesn’t it allow for date and month only? For 6 digit
> fractions of seconds? Or for date-time with timezones? How is matching
> done then (e.g., Z vs +00:00)?

3.  The DICOM element
    ParticipantObjectIdentification.ParticipantObjectDescription it is
    defined as a complex type but FHIR AuditEvent.entity.description it
    is a string element. How should we handle this mapping?

> **Decision:** The guideline is to not use this element since in R5 it
> will not be present anymore (see
> [<u>https://gforge.hl7.org/gf/project/fhir/tracker/?action=TrackerItemEdit&tracker_item_id=2</u>](https://gforge.hl7.org/gf/project/fhir/tracker/?action=TrackerItemEdit&tracker_item_id=20888)
> [<u>0888</u>](https://gforge.hl7.org/gf/project/fhir/tracker/?action=TrackerItemEdit&tracker_item_id=20888))
> because ParticipantObjectDescription is simply a grouper element and
> thus cannot hold any value.

4.  In
    [<u>https://www.hl7.org/fhir/R4/auditevent-mappings.html#dicom</u>](https://www.hl7.org/fhir/R4/auditevent-mappings.html#dicom)
    the EventDateTime it is mapped in AuditEvent.period but should be
    mapped in AuditEvent.recorded. How should we handle this?

> **Decision:** In future release of FHIR, R5, this issue will be
> resolved (see
> [<u>https://gforge.hl7.org/gf/project/fhir/tracker/?action=TrackerItemEdit&tracker_id=677&t</u>](https://gforge.hl7.org/gf/project/fhir/tracker/?action=TrackerItemEdit&tracker_id=677&tracker_item_id=20837)
> [<u>racker_item_id=20837</u>](https://gforge.hl7.org/gf/project/fhir/tracker/?action=TrackerItemEdit&tracker_id=677&tracker_item_id=20837)).
> In the meantime, in Table 3.81.4.2.2.1-1 there is the mapping to be
> used.

5.  AuditEvent resource does not address the PRI syslog data field. How
    should we handle this?

> **Decision:** In future release of FHIR, R5, this issue will be
> resolved (see
> [<u>https://gforge.hl7.org/gf/project/fhir/tracker/?action=TrackerItemEdit&tracker_item_id=1</u>](https://gforge.hl7.org/gf/project/fhir/tracker/?action=TrackerItemEdit&tracker_item_id=18088&start=11600)
> [<u>8088&start=11600</u>](https://gforge.hl7.org/gf/project/fhir/tracker/?action=TrackerItemEdit&tracker_item_id=18088&start=11600))

## Closed Issues

1.  How can we address integration statement for new actors that
    supports \[ITI-20\]?

> **Decision:** A set of options have been added in order to declare the
> protocol used by Secure Node, Secure Application, Audit Record
> Forwarder.

2.  How to deal with different protocols defined in \[ITI-20\]?

> **Decision:** The Record Audit Event \[ITI-20\] transaction it has
> been modified to support POST of single AuditEvent resources or a
> Bundle of them. To send a Bundle of AuditEvent it is required to use
> the “batch” interaction (see
> [https://www.hl7.org/fhir/R4/http.html#transaction).](https://www.hl7.org/fhir/R4/http.html#transaction))

3.  In
    [<u>https://www.hl7.org/fhir/R4/auditevent-mappings.html#dicom</u>](https://www.hl7.org/fhir/R4/auditevent-mappings.html#dicom)
    the ActiveParticipant.RoleIdCode it is mapped either in
    AuditEvent.agent.type and AuditEvent.agent.role. How should we
    handle the mapping?

> **Decision:** The guideline is to map the RoleIdCode in the agent.role
> element, if the code is known by the ARR as a type should be mapped in
> the agent.type element instead. When FHIR Release 5 will be aligned
> with this decision see CP \#20536
> <https://gforge.hl7.org/gf/project/fhir/tracker/?action=TrackerItemEdit&tracker_item_id=2>
>
> 200
>
> 205
>
> 210
>
> 215
>
> 220
>
> 225
>
> 230
>
> 235
>
> 0536&start=0 update Section [3.81.4.2.2.1 Mapping between DICOM and
> FHIR](#mapping-between-fhir-and-dicom-for-query-interaction) removing
> the statement.

4.  The mapping defined in
    [<u>https://www.hl7.org/fhir/R4/auditevent-mappings.html#dicom</u>](https://www.hl7.org/fhir/R4/auditevent-mappings.html#dicom)
    it is not sufficient in order to allow auditing through the
    AuditEvent Resource.

> **Decision:** in Section 3.81.4.2.2.1 the mapping defined by FHIR has
> been further constrained in order to allow interoperability between
> the two data models.

5.  Should the server be required to error for lack of a time period in
    \[ITI-81\] and \[ITI-82\] or should this be weakened to “should” or
    “recommend” or “may”?

> **Decision:** the server is not required to reject a request. It could
> do so, in accordance to the specification.

6.  Should support of the “/.well-known/” path RFC5785 be required or
    described in transactions \[ITI-81\] and \[ITI-82\]? (This can be an
    alternative to more complete server information.) For example, PACS
    servers providing restful access to DICOM objects may respond to
    “/.well-known/DICOM” in addition to a fully specified URL path.

> **Decision:** the functionality is covered by the Capability
> Statement.

7.  Only a JSON return format is specified for Retrieve Syslog Messages
    \[ITI-82\] (non FHIR transaction). It delivers a slightly parsed
    form of the syslog message that makes JSON attributes in a structure
    that corresponds to the structure define by syslog. Should other
    forms be supported? Should the unparsed syslog message be returned?

> **Decision:** During public comment and during TI period no vendors
> raise issues about the format of this transaction.

8.  Should a server information query be specified? There are various
    RFCs from the IETF that specify aspects of server information.

> **Decision:** now FHIR allows the definition of conformance resources.
> We defined them and they can be found in the IHE/fhir github
> repository.

9.  This supplement is being written as additions to the ITI TF-1:9,
    ATNA, which was written to an older outline template. Rather than
    redocument ATNA entirely, these sections are added using that
    outline, not the new template. The new sections all fit
    appropriately into either outline.

> The Report Audit Event Transaction \[ITI-20\] is completely rewritten
> to the current template outline. It was old and written to a very
> different outline than the current template structure. Merging in the
> options and their effect on this transaction became very confusing.
>
> The Node Authentication Transaction \[ITI-19\] is not affected by this
> supplement.

10. What audit event log sources should be defined to be supported by
    the query transaction? The table below is a partial list of event
    sources. This list is the combination of event sources supported by
    a variety of event management software.

> 240
>
> 245
>
> 250
>
> **Decision:** this version will only mandate support for the IHE ATNA
> formats the generic SYSLOG format and the FHIR AuditEvent format. The
> many other formats and transports can be added later as options or by
> vendors as product options.
>
> Examination of a variety of event reporting and logging products
> resulted in the following list of sources. After discussion and given
> scope concerns, no additional sources or encodings will be described.

**Partial List of event sources/codecs considered**

<table style="width:68%;">
<colgroup>
<col style="width: 34%" />
<col style="width: 34%" />
</colgroup>
<thead>
<tr>
<th><blockquote>
<p><strong>Name of source</strong></p>
</blockquote></th>
<th style="text-align: center;"><strong>Decision</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>IHE ATNA</td>
<td>Support</td>
</tr>
<tr>
<td>Collectd</td>
<td>No (perhaps future)</td>
</tr>
<tr>
<td>Elasticsearch</td>
<td>No (perhaps future)</td>
</tr>
<tr>
<td>Eventlog</td>
<td>No (perhaps future)</td>
</tr>
<tr>
<td>Imap</td>
<td>No (perhaps future)</td>
</tr>
<tr>
<td>Log4j</td>
<td>No (perhaps future)</td>
</tr>
<tr>
<td>Lumberjack</td>
<td>No (perhaps future)</td>
</tr>
<tr>
<td>S3</td>
<td>No (perhaps future)</td>
</tr>
<tr>
<td>Snmp</td>
<td>No (perhaps future)</td>
</tr>
<tr>
<td><blockquote>
<p>Syslog</p>
</blockquote></td>
<td><blockquote>
<p>Support</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>Twitter firehose</p>
</blockquote></td>
<td><blockquote>
<p>No (perhaps future)</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>Xmpp</p>
</blockquote></td>
<td><blockquote>
<p>No (perhaps future)</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>Zeromq</p>
</blockquote></td>
<td><blockquote>
<p>No (perhaps future)</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>Edn</p>
</blockquote></td>
<td><blockquote>
<p>No (perhaps future)</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>Fluent</p>
</blockquote></td>
<td><blockquote>
<p>No (perhaps future)</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>Json</p>
</blockquote></td>
<td><blockquote>
<p>No (perhaps future)</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>Spool</p>
</blockquote></td>
<td><blockquote>
<p>No (perhaps future)</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>FHIR</p>
</blockquote></td>
<td><blockquote>
<p>Support</p>
</blockquote></td>
</tr>
</tbody>
</table>

11. Event transports were selected as part of the planning decision for
    this work item. Technical evaluation found no issues with it.

<table style="width:99%;">
<colgroup>
<col style="width: 32%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr>
<th><blockquote>
<p><strong>Name of source</strong></p>
</blockquote></th>
<th><blockquote>
<p><strong>Short Description</strong></p>
</blockquote></th>
<th style="text-align: center;"><strong>Issues</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>IHE ATNA</td>
<td><blockquote>
<p>Covered in this supplement</p>
</blockquote></td>
<td>None</td>
</tr>
<tr>
<td>Syslog</td>
<td><blockquote>
<p>Covered in this supplement</p>
</blockquote></td>
<td>None</td>
</tr>
<tr>
<td>FHIR</td>
<td><blockquote>
<p>Covered in this supplement</p>
</blockquote></td>
<td>None</td>
</tr>
</tbody>
</table>

12. Candidate Query “standards”

> A variety of existing event management products and standards were
> examined. Most of the existing system use product specific plug-ins,
> direct database access, or other methods for providing query access.
>
> After review, four candidates were considered worth further
> evaluation.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr>
<th><blockquote>
<p><strong>Name of source</strong></p>
</blockquote></th>
<th><blockquote>
<p><strong>Short Description</strong></p>
</blockquote></th>
<th style="text-align: center;"><strong>Decision</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>DCM4CHE</td>
<td>Open Source implementation of PACS archive including ARR as well as
much else. At least 5,000 operational downloads, but most probably not
for ARR use.</td>
<td><blockquote>
<p>Evaluate</p>
</blockquote></td>
</tr>
<tr>
<td>Tiani Spirit EHR (awaiting formal name)</td>
<td>EU Public specification. Implementation underway.</td>
<td><blockquote>
<p>Evaluate</p>
</blockquote></td>
</tr>
<tr>
<td>Connect / Healtheway/ ?</td>
<td>Published specification. Need to determine license, etc., but
probably suitable.</td>
<td><blockquote>
<p>Evaluate</p>
</blockquote></td>
</tr>
<tr>
<td>FHIR AuditEvent Report</td>
<td>Query of a FHIR resource</td>
<td><blockquote>
<p>Evaluate</p>
</blockquote></td>
</tr>
<tr>
<td>Plug-in style (multiple)</td>
<td>A variety of product specific mechanisms to write plug-ins for that
product.</td>
<td><blockquote>
<p>Reject, too product specific, subject to change at will by product
vendor</p>
</blockquote></td>
</tr>
<tr>
<td>Direct access to database (multiple)</td>
<td><blockquote>
<p>A variety of product specific mechanisms that document the format and
access methods for the internal database used by the product.</p>
</blockquote></td>
<td><blockquote>
<p>Reject, too product specific, subject to change at will by product
vendor</p>
</blockquote></td>
</tr>
<tr>
<td>Direct access to flat files (multiple)</td>
<td>A variety of product specific mechanisms that document the format
and access methods for flat files of messages created by the
product.</td>
<td><blockquote>
<p>Reject, too product specific, subject to change at will by product
vendor</p>
</blockquote></td>
</tr>
</tbody>
</table>

> The surviving four were evaluated against the ITI list of evaluation
> criteria. The general spreadsheet was reviewed and the following table
> is the result.
>
> **Evaluation Criteria Results**

<table style="width:100%;">
<colgroup>
<col style="width: 22%" />
<col style="width: 18%" />
<col style="width: 17%" />
<col style="width: 24%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr>
<th><blockquote>
<p><strong>Criteria</strong></p>
</blockquote></th>
<th><blockquote>
<p><strong>DCM4CHE</strong></p>
</blockquote></th>
<th><blockquote>
<p><strong>Tiani Spirit EHR</strong></p>
</blockquote></th>
<th><strong>Connect/Healtheway</strong></th>
<th style="text-align: center;"><p><strong>FHIR</strong></p>
<p><strong>(AuditEvent)</strong></p></th>
</tr>
</thead>
<tbody>
<tr>
<td>Stability</td>
<td></td>
<td>Early development</td>
<td>Has been deprecated</td>
<td>STU and Normative</td>
</tr>
<tr>
<td>From an SDO</td>
<td>No</td>
<td>Govt specification</td>
<td>Govt specification</td>
<td>Yes</td>
</tr>
<tr>
<td>Licensing restrictions</td>
<td>LGPL v2</td>
<td></td>
<td>?</td>
<td>CC 0</td>
</tr>
<tr>
<td>Implementation Experience</td>
<td>Approx 5K installations</td>
<td></td>
<td></td>
<td>Hackathons, Connectathons</td>
</tr>
<tr>
<td>Ease of adoption</td>
<td>Open Source</td>
<td></td>
<td></td>
<td>Will be easy</td>
</tr>
<tr>
<td>RESTful/SOAP/other</td>
<td>RESTful</td>
<td>SOAP</td>
<td></td>
<td>RESTful</td>
</tr>
<tr>
<td>ATNA specific query</td>
<td>Yes</td>
<td>Yes</td>
<td>Yes</td>
<td>Kind-of</td>
</tr>
<tr>
<td>Generic SYSLOG query</td>
<td>No</td>
<td>No</td>
<td>No</td>
<td>No</td>
</tr>
<tr>
<td>Phase 1 decision</td>
<td>Continue evaluation</td>
<td>Drop</td>
<td>Drop</td>
<td>Continue evaluation</td>
</tr>
<tr>
<td>Acceptance by Intrusion Detection/ Security Analysis vendors</td>
<td>?</td>
<td>n.a.</td>
<td>n.a.</td>
<td>?</td>
</tr>
</tbody>
</table>

> 255
>
> 260
>
> 265
>
> 270
>
> 275
>
> 280
>
> 285
>
> 290
>
> **Decision:** FHIR was selected as the standard to be used to profile
> the Query transaction. The FHIR event report is managed as a joint
> effort among HL7 FHIR, IHE, and DICOM. This makes coordination of the
> necessary resource changes fairly straightforward.
>
> In order to use FHIR the following modification/extension/addition to
> the query will be needed:

- We need the same functional capabilities as DCM4CHE. The large
  installed base of DCM4CHE indicates that the functionality is widely
  needed. Adapting this functionality to use a FHIR query is a
  reasonable change if the functional capabilities do not need to change
  significantly.

- The generic Syslog query will not fit a FHIR query. This was made
  optional and a simple query that is similar to FHIR was defined.

> The major risk item is coordinating release and preparation schedules.
> In order to fit HL7 publication schedule a reasonable version of the
> resource and query are needed by 22 March 2015. Revisions based upon
> public comment and TI experience can be handled during the FHIR DSTU
> cycle.

13. Should we define an actor and transaction for the other syslog
    messages that are not ATNA schema compliant? Should we mandate
    support for this kind of message from any secure actor? From any
    secure node? Or, should these filtering these messages only be
    mandated when originating on an ATNA compliant node, and support for
    other nodes be left as a product option?

> **Decisions**: The Filter and Forward transaction explicitly state
> that syslog messages not compliant with ATNA schema can be received.
> Those messages should be sent using the same protocol requirement
> defined for ATNA. This was addressed in the \[ITI-20\] rewrite.
>
> The query for generic syslog messages was defined and is similar to
> FHIR in some respects. It is made optional.

14. Should Audit Record Repository always be required grouping with
    secure node/application or only when it does forwarding? ARR often
    have lots of PHI, so secure node may be generally appropriate. What
    about all the other syslog uses? **Decision**: Not needed the SN/SA
    grouping for the store/forward option. The text in the options
    section is sufficient. We have the need to track the Query event
    without using all the requirements introduced by the SN grouping, so
    there is no requirement to send the audit to another repository via
    TLS.

15. The Retrieve Syslog Message \[ITI-82\] only mandates support for
    query to return all syslog messages with timestamps within a time
    window. Should any other queries be mandated?

### Decision: NO

16. The query option is silent about how the Audit Record Repository
    determines which syslog messages are stored for later query, how
    long messages remain available for query, etc. Should there be any
    requirements put on this? The motivation for this is the

> 295
>
> 300
>
> 305
>
> 310
>
> 315
>
> 320
>
> 325
>
> 330
>
> wide range of real world situations, ranging from sites that must
> process tens of thousands of syslog messages per second to sites that
> manage a few hundred per day. Some sites deal only with major level
> ATNA security events. Some sites deal with syslog reports of every
> network connection, ping, firewall warning, etc. **Decision:** New
> \[ITI-20\] makes it clear that these issues are decided during
> implementation and deployment.

17. Have two endpoints - one for syslog, one for ATNA? Have one and let
    parameters separate? Have two and permit ATNA parameters on syslog?
    Have two and permit syslog parameters ATNA (FHIR will generate 400 -
    bad request unless there is a FHIR extension defined)?

> **Decision:** two endpoints, one FHIR based and one for generic
> syslog.

18. Should Audit Record Repository always be required grouping with
    secure node/application or only when it does forwarding? ARR often
    have lots of PHI, so secure node may be generally appropriate. What
    about all the other syslog uses?

> ***Considerations:*** The logging of the query event is clearly
> appropriate. However, there are requirements introduced by the ATNA
> Secure Node that are not applicable to our scenario where the Audit
> Source IS the Audit Record Repository itself: the ARR is required to
> send audit records via UDP or TLS. We SHOULD mandate the creation of
> audit records structured in accordance to ATNA structure and no other
> transport requirements. There is another point to take in
> consideration: once the ATNA query is made, an audit record is
> created. Should this audit be returned into the same transaction
> (query Response)?
>
> **Decision:** This is a very important implementation decision, and
> IHE cannot define requirement for this.

19. Transaction \[ITI-81\] is based on a FHIR query operation. Not all
    the search parameters defined in this transaction are actually
    standard FHIR search parameters. A CP to FHIR is submitted to add
    “outcome” and “role” as standard search parameters (CP \#9919
    [http://gforge.hl7.org/gf/project/fhir/DSTU2/tracker/?action=TrackerItemEdit&tracker_ite](http://gforge.hl7.org/gf/project/fhir/tracker/?action=TrackerItemEdit&tracker_item_id=9919)
    [m_id=9919](http://gforge.hl7.org/gf/project/fhir/tracker/?action=TrackerItemEdit&tracker_item_id=9919)).

> **Decision:** This issue was resolved with STU3 release.

20. Tech cmte has documented the query to patient.identifier, starting
    from a search parameter of type “reference”. Does this reflect the
    FHIR requirements in the correct way?

> **Decision:** Starting from STU3 release it’s well understood how to
> use search parameters of type reference to navigate through resources.

21. CP-ITI-1152 asks for an enhancement of the patient.identifier search
    parameter to search also for audit where the patient is involved in
    the event as a participant.

> **Decision:** During the update to move this supplement to FHIR R4 the
> CP was included in order to have an alignment between the search
> parameters, defined by FHIR and the ones defined in this supplement
> that can be used to search for patient involved in the event either as
> a user and either as a participant.
>
> 335
>
> 340

22. This Supplement provides two different tables in order to provide
    distinct mapping for the feed (see Table 3.20.4.2.2.1) and for the
    query (see 3.81.4.2.2.1) transactions. Mapping for the query is
    intended to be normative. On the other side the mapping for the feed
    is provided for implementers that needs guidelines on how to map
    Audit Message info listed in TF into an AuditEvent Resource and
    should not be considered normative.

23. The new FHIR feed mechanism that can be used by Secure Node Secure
    Application ad Audit Record Forwarder enables subscription
    mechanisms. Should we profile this subscription mechanism?

> **Decision**: During Public Comment no feedback were received about
> this issue, thus we decided to move approve the supplement for TI
> without addressing this issue.
>
> 345
>
> 350
>
> 355

##  IHE Technical Frameworks General Introduction

> The [<u>IHE Technical Framework General
> Introduction</u>](https://profiles.ihe.net/GeneralIntro) is shared by
> all of the IHE domain technical frameworks. Each technical framework
> volume contains links to this document where appropriate.

## 9 Copyright Licenses

> IHE technical documents refer to, and make use of, a number of
> standards developed and published by several standards development
> organizations. Please refer to the IHE Technical Frameworks General
> Introduction, [<u>Chapter 9 - Copyright
> Licenses</u>](https://profiles.ihe.net/GeneralIntro/ch-9.html) for
> copyright license information for frequently referenced base
> standards. Information pertaining to the use of IHE International
> copyrighted materials is also available there.

## 10 Trademark

> IHE<sup>®</sup> and the IHE logo are trademarks of the Healthcare
> Information Management Systems Society in the United States and
> trademarks of IHE Europe in the European Community. Please refer to
> the IHE Technical Frameworks General Introduction, [<u>Chapter 10 -
> Trademark</u>](https://profiles.ihe.net/GeneralIntro/ch-10.html) for
> information on their use.

## 360 IHE Technical Frameworks General Introduction Appendices

> The [<u>IHE Technical Framework General Introduction
> Appendices</u>](https://profiles.ihe.net/GeneralIntro/index.html) are
> components shared by all of the IHE domain technical frameworks. Each
> technical framework volume contains links to these documents where
> appropriate.
>
> *Update the following appendices to the General Introduction as
> indicated below. Note that these are **not** appendices to this
> domain’s Technical Framework (TF-1, TF-2, TF-3 or TF-4) but rather,
> they are appendices to the IHE Technical Frameworks General
> Introduction located
> [<u>here</u>.](https://profiles.ihe.net/GeneralIntro/index.html)*

## 370 [<u>Appendix A</u>](https://profiles.ihe.net/GeneralIntro/ch-A.html) – Actors

> *Add the following **new or modified** actors to the [<u>IHE Technical
> Frameworks
> General</u>](https://profiles.ihe.net/GeneralIntro/ch-A.html)
> [<u>Introduction Appendix
> A</u>](https://profiles.ihe.net/GeneralIntro/ch-A.html):*

<table>
<colgroup>
<col style="width: 32%" />
<col style="width: 67%" />
</colgroup>
<thead>
<tr>
<th style="text-align: center;"><strong>Actor</strong></th>
<th style="text-align: center;"><strong>Definition</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td><blockquote>
<p>Audit Consumer</p>
</blockquote></td>
<td><blockquote>
<p>Queries for audit record content.</p>
</blockquote></td>
</tr>
</tbody>
</table>

## 375 [<u>Appendix B</u>](https://profiles.ihe.net/GeneralIntro/ch-B.html) – Transactions

> *Add the following **new or modified** transactions to the [<u>IHE
> Technical Frameworks
> General</u>](https://profiles.ihe.net/GeneralIntro/ch-B.html)
> [<u>Introduction Appendix
> B</u>](https://profiles.ihe.net/GeneralIntro/ch-B.html):*

<table>
<colgroup>
<col style="width: 32%" />
<col style="width: 67%" />
</colgroup>
<thead>
<tr>
<th><blockquote>
<p><strong>Transaction</strong></p>
</blockquote></th>
<th style="text-align: center;"><strong>Definition</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td><blockquote>
<p>Retrieve ATNA Audit Event [ITI-81]</p>
</blockquote></td>
<td><blockquote>
<p>Retrieve Audit Records. Search ATNA audit records based upon queries
using ATNA audit record content.</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>Retrieve Syslog Event [ITI-82]</p>
</blockquote></td>
<td><blockquote>
<p>Retrieve Syslog Messages. Search syslog messages based upon using the
syslog metadata.</p>
</blockquote></td>
</tr>
</tbody>
</table>

> 380

## [<u>Appendix D</u>](https://profiles.ihe.net/GeneralIntro/ch-D.html) – Glossary

> *Add the following **new or modified glossary** terms to the [<u>IHE
> Technical Frameworks
> General</u>](https://profiles.ihe.net/GeneralIntro/ch-D.html)
> [<u>Introduction Appendix
> D</u>](https://profiles.ihe.net/GeneralIntro/ch-D.html):*

<table>
<colgroup>
<col style="width: 32%" />
<col style="width: 67%" />
</colgroup>
<thead>
<tr>
<th><blockquote>
<p><strong>Glossary Term</strong></p>
</blockquote></th>
<th style="text-align: center;"><strong>Definition</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td><blockquote>
<p>Audit Record</p>
</blockquote></td>
<td><blockquote>
<p>A syslog message that complies with the DICOM PS3.15 schema.</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>Syslog message</p>
</blockquote></td>
<td><blockquote>
<p>Any message that complies with RFC5424, regardless of the format of
the message body. An ATNA audit log message is a specific kind of syslog
message that has a specific format for the message body.</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>Syslog metadata</p>
</blockquote></td>
<td><blockquote>
<p>Attributes that classify the audit record: defining severity of the
event, facility, and application that sent the message. These are
defined in RFC5424.</p>
</blockquote></td>
</tr>
</tbody>
</table>

# Volume 1 – Profiles

> 390
>
> 395
>
> 400
>
> 405
>
> 410
>
> 415
>
> *Editor: Update [<u>Section
> 9</u>](https://profiles.ihe.net/ITI/TF/Volume1/ch-9.html) adding the
> following text at the end of that section:*

## 9 Audit Trail and Node Authentication (ATNA)

> The Audit Trail and Node Authentication (ATNA) Profile specifies the
> foundational elements needed by all forms of secure systems: node
> authentication, user authentication, event logging (audit), and
> telecommunications encryption. It is also used to indicate that other
> internal security properties such as access control, configuration
> control, and privilege restrictions are provided.
>
> Many other IHE profiles require or recommend grouping with ATNA actors
> as part of their security considerations.
>
> **<u>The ATNA Profile defines capabilities to both send to and
> retrieve messages from an Audit</u> <u>Record Repository (ARR):</u>**

- **<u>The Record Audit Event \[ITI-20\] transaction enables a Secure
  Node, Secure</u> <u>Application or an Audit Record Forwarder to send a
  single or a group of Audit</u> <u>Records to an Audit Record
  Repository. This transaction supports encodings: syslog</u>
  <u>protocol over TLS, syslog protocol over UDP, or an HTTP POST of
  FHIR</u> <u>AuditEvent Resources.</u>**

- **<u>The Retrieve ATNA Audit Event \[ITI-81\] transaction enables an
  Audit Consumer</u> <u>to retrieve ATNA audit records stored within an
  Audit Record Repository. This</u> <u>transaction is based on a FHIR
  RESTful search operation on AuditEvent</u> <u>Resources.</u>**

- **<u>The Retrieve Syslog Event \[ITI-82\] transaction enables an Audit
  Consumer to</u> <u>search syslog messages stored in an Audit Record
  Repository. This transaction is</u> <u>defined as a RESTful operation.
  The search parameters are based on syslog</u> <u>metadata.</u>**

> **<u>Note that audit events sent to the Audit Record Repository using
> Syslog protocol may not</u> <u>conform to ATNA Audit Events, so the
> Retrieve Syslog Event \[ITI-82\] transaction enables</u> <u>retrieval
> of audit records based on syslog metadata values.</u>**
>
> *Editor: Update Figure 9.1-1 as follows. Note that in the figure
> below, the existing actors and transactions are shown in dashed lines.
> The figure should be updated by adding the actors and transactions in
> solid lines: Audit Consumer, Retrieve ATNA Audit Event, Retrieve
> Syslog Event.*
>
> 420

<table style="width:47%;">
<colgroup>
<col style="width: 22%" />
<col style="width: 24%" />
</colgroup>
<thead>
<tr>
<th rowspan="2"></th>
<th><blockquote>
<p>Audit Record Repository</p>
</blockquote></th>
</tr>
<tr>
<th rowspan="2">Audit Record Forwarder</th>
</tr>
<tr>
<th></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

<table style="width:43%;">
<colgroup>
<col style="width: 18%" />
<col style="width: 18%" />
<col style="width: 6%" />
</colgroup>
<thead>
<tr>
<th colspan="2">Retrieve ATNA Audit Event [ITI-81]↑</th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td></td>
<td colspan="2" rowspan="2"><blockquote>
<p>Audit Consumer</p>
</blockquote></td>
</tr>
<tr>
<td></td>
</tr>
</tbody>
</table>

> ![](./media/image2.png)**Figure 9.1-1: Audit Trail and Node
> Authentication Diagram**
>
> *Editor: In [<u>Section
> 9.1</u>,](https://profiles.ihe.net/ITI/TF/Volume1/ch-9.html#9.1)
> Update Table 9.1-1*
>
> 425
>
> **Table 9.1-1: ATNA Profile - Actors and Transactions**

<table style="width:91%;">
<colgroup>
<col style="width: 20%" />
<col style="width: 35%" />
<col style="width: 16%" />
<col style="width: 18%" />
</colgroup>
<thead>
<tr>
<th><blockquote>
<p><strong>Actors</strong></p>
</blockquote></th>
<th><blockquote>
<p><strong>Transactions</strong></p>
</blockquote></th>
<th style="text-align: center;"><strong>Optionality</strong></th>
<th><blockquote>
<p><strong>Reference</strong></p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="3"><blockquote>
<p>Audit Record Repository</p>
</blockquote></td>
<td><blockquote>
<p>Record Audit Event [ITI-20]</p>
</blockquote></td>
<td style="text-align: center;">R</td>
<td><blockquote>
<p>ITI TF-2: 3.20</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p><strong><u>Retrieve ATNA Audit Event [ITI-81]</u></strong></p>
</blockquote></td>
<td style="text-align: center;"><strong><u>O</u></strong></td>
<td><blockquote>
<p><strong><u>ITI TF-2: 3.81</u></strong></p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p><strong><u>Retrieve Syslog Event [ITI-82]</u></strong></p>
</blockquote></td>
<td style="text-align: center;"><strong><u>O</u></strong></td>
<td><blockquote>
<p><strong><u>ITI TF-2: 3.82</u></strong></p>
</blockquote></td>
</tr>
<tr>
<td rowspan="2"><blockquote>
<p><strong><u>Audit Consumer</u></strong></p>
</blockquote></td>
<td><blockquote>
<p><strong><u>Retrieve ATNA Audit Event [ITI-81]</u></strong></p>
</blockquote></td>
<td style="text-align: center;"><strong><u>O</u></strong></td>
<td><blockquote>
<p><strong><u>ITI TF-2: 3.81</u></strong></p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p><strong><u>Retrieve Syslog Event [ITI-82]</u></strong></p>
</blockquote></td>
<td style="text-align: center;"><strong><u>O</u></strong></td>
<td><blockquote>
<p><strong><u>ITI TF-2: 3.82</u></strong></p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>Audit Record Forwarder</p>
</blockquote></td>
<td><blockquote>
<p>Record Audit Event [ITI-20]</p>
</blockquote></td>
<td style="text-align: center;">R</td>
<td><blockquote>
<p>ITI TF-2: 3.20</p>
</blockquote></td>
</tr>
<tr>
<td rowspan="2"><blockquote>
<p>Secure Node</p>
</blockquote></td>
<td><blockquote>
<p>Authenticate Node [ITI-19]</p>
</blockquote></td>
<td style="text-align: center;">R</td>
<td><blockquote>
<p>ITI TF-2: 3.19</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>Record Audit Event [ITI-20]</p>
</blockquote></td>
<td style="text-align: center;">R</td>
<td><blockquote>
<p>ITI TF-2: 3.20</p>
</blockquote></td>
</tr>
<tr>
<td rowspan="2"><blockquote>
<p>Secure Application</p>
</blockquote></td>
<td><blockquote>
<p>Authenticate Node [ITI-19]</p>
</blockquote></td>
<td style="text-align: center;">R</td>
<td><blockquote>
<p>ITI TF-2: 3.19</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>Record Audit Event [ITI-20]</p>
</blockquote></td>
<td style="text-align: center;">R</td>
<td><blockquote>
<p>ITI TF-2: 3.20</p>
</blockquote></td>
</tr>
</tbody>
</table>

> *Editor: Update [<u>Section
> 9.1.1.3</u>](https://profiles.ihe.net/ITI/TF/Volume1/ch-9.html#9.1.1.3)
> as follows:*
>
> 430
>
> 435
>
> 440
>
> 445
>
> 450

###  Audit Record Repository

> The Audit Record Repository receives event audit reports and stores
> them. It may be part of a federated network of repositories. It is
> expected to have analysis and reporting capabilities, but those
> capabilities are not specified as part of this profile. This profile
> does not specify the capacity of an Audit Record Repository, because
> the variety of deployment needs makes it impractical to set
> requirements for the event report volume or capacity needed.
>
> The Audit Repository shall support:

1.  At least one of the audit transport mechanisms specified in [<u>ITI
    TF-2: 3.20</u>](https://profiles.ihe.net/ITI/TF/Volume2/ITI-20.html)
    (see Table 9.2-1).

2.  Receipt of at least one of the IHE-specified audit message formats.
    Note that the message format is extensible to include both future
    IHE specifications (e.g., audit requirements for new IHE
    transactions) and private extensions.

3.  Local security and privacy service protections and user access
    controls.

> The Audit Record Repository may ignore or process messages in non-IHE
> message formats. This may be for backwards compatibility or other
> reasons.
>
> The Audit Record Repository be grouped with a Secure Node or Secure
> Application.

### <u>The Audit Record Repository may support search capabilities as defined in ITI TF-2: 3.81</u> <u>and 3.82</u>

> **<u>Audit Record Repository may support search capabilities as
> defined in ITI TF-2: 3.81 and</u> <u>3.82.</u>**
>
> *Editor: Add **new** Section 9.1.1.5*

### 9.1.1.5 Audit Consumer

> The Audit Consumer queries an Audit Record Repository for syslog and
> ATNA audit records using Syslog metadata and ATNA audit record
> content. Subsequent processing of the query
>
> 455 result is not defined in this profile.
>
> *Editor: Update [<u>ITI
> TF-1:9.2</u>](https://profiles.ihe.net/ITI/TF/Volume1/ch-9.html#9.2)
> as shown, including the note under Table 9.2-1.*
>
> 460
>
> 465
>
> 470

##  9.2 ATNA Actor Options

> Options that may be selected for this Integration Profile are listed
> in the Table 9.2-1 along with the actors to which they apply.
> Dependencies between options when applicable are specified in notes.
>
> Note: The “ATX” prefix in option names below marks alternatives for
> audit transport protocol, and the “STX” prefix marks alternatives for
> secure transport protocol, as defined in the Record Audit Event
> \[ITI-20\] transaction.
>
> **Table 9.2-1: ATNA – Actors and Options**

<table>
<colgroup>
<col style="width: 30%" />
<col style="width: 33%" />
<col style="width: 36%" />
</colgroup>
<thead>
<tr>
<th style="text-align: center;"><strong>Actor</strong></th>
<th><blockquote>
<p><strong>Option Name</strong></p>
</blockquote></th>
<th><blockquote>
<p><strong>Vol. &amp; Section</strong></p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="5"><blockquote>
<p>Audit Record Repository (Note 4)</p>
</blockquote></td>
<td><blockquote>
<p><strong><u>Retrieve Audit Message</u></strong></p>
</blockquote></td>
<td><blockquote>
<p><strong><u>ITI TF-1: 9.2.3</u></strong></p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p><strong><u>Retrieve Syslog Message</u></strong></p>
</blockquote></td>
<td><blockquote>
<p><strong><u>ITI TF-1: 9.2.4</u></strong></p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p><strong><u>ATX: FHIR Feed</u></strong></p>
</blockquote></td>
<td><blockquote>
<p><strong><u>ITI TF-1: 9.2.7.1</u></strong></p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>ATX: TLS Syslog</p>
</blockquote></td>
<td><blockquote>
<p>ITI TF-1: 9.2.7.2</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>ATX: UDP Syslog</p>
</blockquote></td>
<td><blockquote>
<p>ITI TF-1: 9.2.7.3</p>
</blockquote></td>
</tr>
<tr>
<td rowspan="2"><blockquote>
<p><strong><u>Audit Consumer</u></strong></p>
</blockquote></td>
<td><blockquote>
<p><strong><u>Retrieve Audit Message (Note 5)</u></strong></p>
</blockquote></td>
<td><blockquote>
<p><strong><u>ITI TF-1: 9.2.3</u></strong></p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p><strong><u>Retrieve Syslog Message (Note 5)</u></strong></p>
</blockquote></td>
<td><blockquote>
<p><strong><u>ITI TF-1: 9.2.4</u></strong></p>
</blockquote></td>
</tr>
<tr>
<td rowspan="3"><blockquote>
<p>Audit Record Forwarder (Note 4)</p>
</blockquote></td>
<td><blockquote>
<p><strong><u>ATX: FHIR Feed</u></strong></p>
</blockquote></td>
<td><blockquote>
<p><strong><u>ITI TF-1: 9.2.7.1</u></strong></p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>ATX: TLS Syslog</p>
</blockquote></td>
<td><blockquote>
<p>ITI TF-1: 9.2.7.2</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>ATX: UDP Syslog</p>
</blockquote></td>
<td><blockquote>
<p>ITI TF-1: 9.2.7.3</p>
</blockquote></td>
</tr>
<tr>
<td rowspan="5"><blockquote>
<p>Secure Node (Note 1)</p>
<p>(Note 4)</p>
</blockquote></td>
<td><blockquote>
<p>Radiology Audit Trail</p>
</blockquote></td>
<td><blockquote>
<p>RAD TF-1: 2.2.1</p>
<p>RAD TF-3: 5.1</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>…</p>
</blockquote></td>
<td><blockquote>
<p>…</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p><strong><u>ATX: FHIR Feed</u></strong></p>
</blockquote></td>
<td><blockquote>
<p><strong><u>ITI TF-1: 9.2.7.1</u></strong></p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>ATX: TLS Syslog</p>
</blockquote></td>
<td><blockquote>
<p>ITI TF-1: 9.2.7.2</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>ATX: UDP Syslog</p>
</blockquote></td>
<td><blockquote>
<p>ITI TF-1: 9.2.7.3</p>
</blockquote></td>
</tr>
<tr>
<td rowspan="5"><blockquote>
<p>Secure Application (Note 1)</p>
<p>(Note 4)</p>
</blockquote></td>
<td><blockquote>
<p>Radiology Audit Trail</p>
</blockquote></td>
<td><blockquote>
<p>RAD TF-1: 2.2.1</p>
<p>RAD TF-3: 5.1</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>…</p>
</blockquote></td>
<td><blockquote>
<p>…</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p><strong><u>ATX: FHIR Feed</u></strong></p>
</blockquote></td>
<td><blockquote>
<p><strong><u>ITI TF-1: 9.2.7.1</u></strong></p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>ATX: TLS Syslog</p>
</blockquote></td>
<td><blockquote>
<p>ITI TF-1: 9.2.7.2</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>ATX: UDP Syslog</p>
</blockquote></td>
<td><blockquote>
<p>ITI TF-1: 9.2.7.3</p>
</blockquote></td>
</tr>
</tbody>
</table>

> …
>
> Note 4: This actor shall support at least one of the “ATX” Options. If
> a product’s IHE Integration Statement does not declare one of these
> options, the reader should assume that the product supports the TLS or
> UDP Syslog Option.
>
> **<u>Note 5: The Audit Consumer shall support at least one of the two
> options defined.</u>**
>
> *Editor: Add **new** Sections 9.2.3 and 9.2.4 to [<u>ITI
> TF-1:9.2</u>](https://profiles.ihe.net/ITI/TF/Volume1/ch-9.html#9.2):*
>
> 475
>
> 480
>
> 485
>
> 490

###  Retrieve Audit Message Option

> The Retrieve Audit Message Option enables search requests for audit
> records based upon message contents.
>
> An Audit Consumer or Audit Record Repository that supports this option
> shall implement the Retrieve ATNA Audit Event \[ITI-81\] transaction.
>
> The \[ITI-81\] transaction is a RESTful search from an Audit Consumer
> to an Audit Record Repository (ARR) using FHIR resources. The search
> response will reflect the contents of the data storage at the time of
> the search. IHE does not specify the criteria for message selection,
> archival, retention interval, etc. These are set by local policy and
> are often different for different Audit Record Repositories.

### Retrieve Syslog Message Option

> The Retrieve Syslog Message Option enables search requests for syslog
> messages based upon syslog metadata.
>
> An Audit Consumer or Audit Record Repository that supports this option
> shall implement the Retrieve Syslog Event \[ITI-82\] transaction.
>
> The \[ITI-82\] transaction is a RESTful search operation that searches
> syslog messages of any format or schema. The search request uses the
> syslog metadata only.
>
> *Editor: Add **new** Section 9.2.7.1 as follows.*
>
> 495
>
> 500

###  Audit Transport (ATX) Options

> At least one of these options shall be supported. Many can be
> declared, for which the product <span id="_bookmark18"
> class="anchor"></span>must then be configurable to enable each of the
> supported Audit Transport Options.

###  <u>ATX: FHIR Feed Option</u>

> **<u>The ATX: FHIR Feed Option enables sending ATNA audit records
> using RESTful</u> <u>capabilities and FHIR resources.</u>**
>
> **<u>An Audit Record Repository that supports this option shall
> implement the two RESTful</u> <u>interactions defined in the Record
> Audit Event \[ITI-20\] transaction. See ITI TF-2: 3.20.4.2</u>
> <u>(Send Audit Resource) and 3.20.4.4 (Send Audit Bundle).</u>**
>
> **<u>A Secure Node, Secure Application or Audit Record Forwarder that
> supports this option</u> <u>shall at least support one of the two
> RESTful interactions defined in the Record Audit</u> <u>Event
> \[ITI-20\] transaction. See ITI TF-2: 3.20.4.2 (Send Audit Resource)
> and 3.20.4.4</u> <u>(Send Audit Bundle).</u>**
>
> 505 <span id="_bookmark19" class="anchor"></span>**9.2.7.2 ATX: TLS
> Syslog Option**
>
> …
>
> *Editor: make the following changes in Table 9.3-1.*
>
> **Table 9.3-1: ATNA - Required Actor Groupings**

<table style="width:98%;">
<colgroup>
<col style="width: 21%" />
<col style="width: 40%" />
<col style="width: 14%" />
<col style="width: 21%" />
</colgroup>
<thead>
<tr>
<th><blockquote>
<p><strong>ATNA Actor</strong></p>
</blockquote></th>
<th><blockquote>
<p><strong>Actor to be grouped with</strong></p>
</blockquote></th>
<th><blockquote>
<p><strong>Reference</strong></p>
</blockquote></th>
<th><blockquote>
<p><strong>Content Bindings Reference</strong></p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="2"><blockquote>
<p>Audit Record Repository</p>
</blockquote></td>
<td><blockquote>
<p>Consistent Time / Time Client</p>
</blockquote></td>
<td><blockquote>
<p>ITI TF-1: 7</p>
</blockquote></td>
<td><blockquote>
<p>N/A</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>ATNA / Secure Node or Secure Application</p>
</blockquote></td>
<td><blockquote>
<p>ITI TF-1: 9</p>
</blockquote></td>
<td><blockquote>
<p>N/A</p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p><strong><u>Audit Consumer</u></strong></p>
</blockquote></td>
<td><blockquote>
<p><strong><u>ATNA / Secure Node or Secure Application</u></strong></p>
</blockquote></td>
<td><blockquote>
<p><strong><u>ITI TF-1: 9</u></strong></p>
</blockquote></td>
<td><blockquote>
<p><strong><u>N/A</u></strong></p>
</blockquote></td>
</tr>
<tr>
<td><blockquote>
<p>…</p>
</blockquote></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

> *Editor: Make the following changes in [<u>Section
> 9.4.2</u>](https://profiles.ihe.net/ITI/TF/Volume1/ch-9.html#9.4.2):*

### Use Cases

> …
>
> **~~In the following paragraphs~~ <u>Sections 9.4.2.1, 9.4.2.2, and
> 9.4.2.3 describe </u>**three typical process flows **~~are
> described~~** for situations in which authorized users, unauthorized
> users, and
>
> 515 unauthorized nodes attempt to gain access to protected health
> information (PHI).

### <u>Sections 9.4.2.4 and 9.4.2.5 describe use cases related to the retrieve capabilities of the</u> <u>Audit Record Repository.</u>

> *Editor: Add **new** Sections 9.4.2.4, 9.4.2.5 and 9.4.3*
>
> 520
>
> 525
>
> 530

###  Clinician Personal History of Study views process flow

> A clinician wants to gather the history of studies she has accessed
> during her clinical activity using different devices (EHR system,
> WebApp, Mobile device). This information allows the clinician to:

- Discover unexpected accesses made to her devices;

- Re-evaluate clinical decisions taken;

- Consolidate on a unique device, a complete picture of complex clinical
  cases.

### Clinician Personal History of Study views use-case

> Dr. Luisa White usually performs her clinical activity using multiple
> devices. Mr. Brown is a patient who is home-monitored. Dr. White
> collects results of home visits using a tablet, and she monthly
> performs a detailed visit with Mr. Brown in her office. During home
> visits, Dr. White
>
> 535
>
> 540
>
> analyzes tele-monitoring data collected by some devices (scales, blood
> pressure devices, etc.) and adjusts drugs therapies in accordance with
> those data. When Dr. White accesses Mr.
>
> Brown’s data via these devices, each access is tracked as an ATNA
> audit event. Both document views and document creation are logged,
> tracking the user that performed the transaction (e.g., using an XUA
> identity assertion).
>
> Monthly visit, Dr. White wants to consolidate within her EHR system
> the whole history of data analyzed and collected using multiple
> devices. This process allows Dr. White to keep track of her clinical
> activities and revaluate clinical decisions made in the past.
>
> To facilitate that, the EHR system can query for audit events related
> to transactions performed by Dr. White during a specific period.
>
> <img src="./media/image4.jpeg"
> style="width:6.58436in;height:4.47969in" />
>
> **Figure 9.4.2.4.1-1: Clinician Personal History of Study views
> process flow**

### Patient access to his audit records process flow

> 545 A patient wants to discover the list of people that accessed a
> specific study. Using those data, the patient discovers if privacy
> policies were correctly applied.
>
> 550
>
> 555
>
> 560

###  Patient access to his audit records use case

> During a hospitalization, Mr. Brown was asked to sign a consent to
> share documents produced during that clinical event with a research
> facility, so that researchers could analyze the efficiency of the
> applied treatment. Mr. Brown does not provide this consent because he
> is worried that his data could be used for marketing purposes. A nurse
> collects the patient’s consent document, but forgets to record his
> decision in the HIS system.
>
> Access to all the data collected during Mr. Brown’s hospitalization by
> clinicians involved in his care are tracked as “Export” or “Disclosure
> events for a “Treatment” purpose. An access to the data by the
> research facility would be tracked as “Export” or “Disclosure” events
> for a “Research” purpose. Mr. Brown’s healthcare facility provides
> on-line access to health information. Mr. Brown can use a web app to
> access this data (shared using XDS or XCA infrastructure). The web app
> can also display audit information related to those documents/studies.
> Audit records are collected by many ATNA Audit Record Repositories,
> but local policies or system configurations allows the web app to
> identify the right Audit Record Repository system that stores relevant
> records. Using the document and study identifiers, the web app can
> query the appropriate ATNA Audit Record Repository.
>
> The web app reports to Mr. Brown that his documents/studies had been
> disclosed or exported for both treatment and research purposes.
>
> 565
>
> 570
>
> 575

<img src="./media/image5.jpeg"
style="width:6.22382in;height:5.37616in" />**Figure 9.4.2.5-1: Patient
access to his audit records Process Flow**

### Technical Approach to Query use cases

> A wide variety of specific reports and analyses may be needed. It is
> assumed there will be a reporting and analysis system with extensive
> database and programmability features. The interoperability need is to
> search suitable subsets of the records held by the Audit Record
> Repository, and to combine and analyze those records to determine a
> final result.
>
> Rather than support a highly complex query capability, ATNA defines
> simple search transactions that can be combined to fit real-world
> needs.
>
> The Retrieve ATNA Audit Event \[ITI-81\] transaction support searches
> based on:

- **Patient identifier**: this search parameter allows discovering all
  of the events that occurred related to a specific patient.

> 580
>
> 585
>
> 590

- **User identifier**: this search parameter allows discovering all of
  the actions performed by a specific user.

- **Object identifier**: this search parameter allows discovering each
  event that occurred related to a specific object (e.g., study,
  reports, image, etc.).

- **Time frame**: this search parameter allows discovering all of the
  events that occurred during a specific time frame.

- **Event type**: this search parameter allows discovering all of the
  occurrences of a specific event (e.g., Data Export, Data Import,
  Query, Authentication, etc.).

- **Application identifier**: this search parameter allows discovering
  all of the events recorded by a specific application or system.

- **Event Outcome Indicator**: this search parameter allows discovering
  all of the events characterized by a specific outcome (e.g., Success,
  Failure, etc.) of the related event.

> For additional analysis beyond that which is fulfilled by the above
> parameters, the Audit Consumer can perform a search for records from
> the time frame expected, and then perform a more detailed analysis on
> those records, locally.
>
> Further details about message semantics are defined in Section ITI
> TF-2: 3.81.
>
> *Editor: Make the following changes in Section 9.5*
>
> 595
>
> 600
>
> 605

##  9.5 ATNA Security Considerations

> **<u>Some basic concepts are described in</u> ~~See~~** Section 9.4.
>
> **<u>ATNA defines transactions for the Audit Record Repository that
> enable sharing of</u> <u>sensitive information related to patients and
> systems.</u>**
>
> **<u>In many implementations and projects, Audit Record Repository
> have been considered a</u> <u>“black-box” able to store relevant
> information for security and monitoring purposes. Those</u> <u>systems
> have not historically been designed to provide external access to
> stored records.</u>**
>
> **<u>Security Officers and System Architects should consider this, and
> analyze the risks of</u> <u>disclosing data stored in the Audit Record
> Repository. The Retrieve ATNA Audit Event</u> <u>\[ITI-81\] and
> Retrieve Syslog Event \[ITI-82\] transactions define how to search
> two</u> <u>categories of audit records:</u>**

- **<u>messages related to IHE transactions or compliant with DICOM
  Audit Message</u> <u>Schema (DICOM PS3.15 Section A.5)</u>
  [<u>http://medical.nema.org/medical/dicom/current/output/chtml/part15/sect_A.5.html</u>](http://medical.nema.org/medical/dicom/current/output/chtml/part15/sect_A.5.html)**.

- **<u>other syslog messages compliant with RFC5424.</u>**

> 610
>
> 615
>
> 620
>
> 625
>
> 630
>
> **<u>Security analysis should consider the content of the other syslog
> messages. The content of</u> <u>those messages is not profiled by IHE
> or DICOM, and may include PHI or other sensitive</u>
> <u>information.</u>**
>
> **<u>Accordingly, access control mechanisms on the ATNA actors and
> queries are strongly</u> <u>recommended. The [Internet User
> Authorization](https://profiles.ihe.net/ITI/TF/Volume1/ch-34.html)
> (IUA) Profile should be considered for the</u> <u>authorization
> controls. The ATNA Audit Record Repository can be grouped with an
> IUA</u> <u>Resource Server to enforce policies and authorization
> decisions. The Audit Consumer can</u> <u>be grouped with an IUA
> Authorization Client to provide authorization information to the</u>
> <u>ATNA Audit Record Repository. Access controls should appropriately
> restrict access to</u> <u>audit records.</u>**
>
> **<u>The Retrieve ATNA Audit Event \[ITI-81\] and Retrieve Syslog
> Event \[ITI-82\] transactions</u> <u>may involve the disclosure of
> sensitive information. Logging these retrieval transactions as</u>
> <u>a query event is appropriate (see ITI TF-2: 3.81.5.1 and 3.82.5.1).
> However, the ATNA</u> <u>Profile does not mandate the grouping of the
> Audit Record Repository with a Secure Node</u> <u>because that
> grouping introduces requirements that are not applicable in this case.
> In</u> <u>particular, it is reasonable that an audit record generated
> by the Audit Record Repository</u> <u>is directly stored within the
> Audit Record Repository database rather than being sent to</u>
> <u>another system using Syslog over TLS protocol. Also, mandating a
> grouping of the Audit</u> <u>Record Repository with a Secure Node
> could lead to audit record feedback loops. The</u> <u>Record Audit
> Event \[ITI-20\] transaction includes some audit requirements for the
> ATNA</u> <u>Audit Record Repository, such as reporting accesses to the
> Audit Record Repository; see</u> <u>[ITI TF-2:
> 3.20.8](https://profiles.ihe.net/ITI/TF/Volume2/ITI-20.html#3.20.8)
> "Disclosures audit message".</u>**
>
> **<u>Additional Security Considerations are described in ITI TF-2:
> Appendix Z.8.</u>**

# Volume 2 – Transactions

> *Editor: update Section 3.20.3 as follows*

## 3.20 Record Audit Event \[ITI-20\]

> <span id="_bookmark29" class="anchor"></span>…

### 3.20.3 Referenced Standards

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 79%" />
</colgroup>
<thead>
<tr>
<th>RFC5424</th>
<th>The Syslog Protocol.</th>
</tr>
</thead>
<tbody>
<tr>
<td>RFC5425</td>
<td>Transmission of Syslog Messages over TLS</td>
</tr>
<tr>
<td>RFC5426</td>
<td>Transmission of Syslog Messages over UDP</td>
</tr>
<tr>
<td>RFC7525</td>
<td>Recommendations for Secure Use of Transport Layer Security (TLS) and
Datagram Transport Layer Security (DTLS)</td>
</tr>
<tr>
<td>DICOM</td>
<td><p>DICOM PS3.15 Annex A.5</p>
<p><a
href="http://medical.nema.org/medical/dicom/current/output/chtml/part15/sect_A.5.html">http://medical.nema.org/medical/dicom/current/output/chtml/part15/sect_A.</a>
<a
href="http://medical.nema.org/medical/dicom/current/output/chtml/part15/sect_A.5.html">5.html</a></p></td>
</tr>
<tr>
<td>ASTM E2147-01</td>
<td>Standard Specification for Audit and Disclosure Logs for Use in
Health Information Systems</td>
</tr>
<tr>
<td>NIST SP 800-92</td>
<td>Guide to Computer Security Log Management.</td>
</tr>
<tr>
<td>W3C XML 1.0</td>
<td>Extensible Markup Language (XML) 1.0</td>
</tr>
<tr>
<td><strong>HL7 FHIR</strong></td>
<td><strong>Release 4 <a
href="http://hl7.org/fhir/R4/index.html"><u>http://hl7.org/fhir/R4/index.html</u></a></strong></td>
</tr>
<tr>
<td><strong><u>RFC4627</u></strong></td>
<td><strong><u>The application/json Media Type for JavaScript Object
Notation</u> <u>(JSON)</u></strong></td>
</tr>
</tbody>
</table>

> 640
>
> *Editor: update Section 3.20.4 adding the new text and interaction
> diagram that shows the two new RESTful interactions*

### Messages

<img src="./media/image6.png" style="width:6.41975in;height:3.50417in"
alt="cp-872-diagram " />

> 645 **Figure 3.20.4-1: Interaction Diagram**
>
> Note 1: Any actor initiating \[ITI-20\] may send to more than one
> Audit Record Repository.
>
> Note 2: The Audit Repository that receives an \[ITI-20\] transaction
> may or may not be grouped with an Audit Record Forwarder. This diagram
> does not show a chain of forwarding between actors.
>
> 650
>
> 655
>
> **<u>Transaction \[ITI-20\] defines three different interactions that
> can be used for auditing:</u>**

1.  **<u>The “Send Audit Event Message - Syslog Interaction” is used for
    auditing using</u> <u>Syslog protocol (see Section 3.20.4.1)</u>**

2.  **<u>The “Send Audit Resource Request Message - FHIR Feed
    Interaction” is used for</u> <u>auditing a single FHIR AuditEvent
    Resource using RESTful protocol (see Section</u> <u>3.20.4.2)</u>**

3.  **<u>The “Send Audit Bundle Request Message - FHIR Feed Interaction”
    is used for</u> <u>auditing a bundle of FHIR AuditEvent Resources
    using RESTful protocol (see</u> <u>Section 3.20.4.4)</u>**

> **<u>The diagram below shows the three interactions that this
> transaction supports:</u>**
>
> **<u>Secure Application, Secure</u> <u>Node, Audit Record
> Forwarder</u>**
>
> **<u>Audit Record</u> <u>Repository</u>**
>
> **<u>Syslog Interaction</u>**
>
> **<u>FHIR Feed Interaction</u>**
>
> **<u>FHIR Feed Interaction</u>**
>
> 660
>
> *Editor: add **new** Sections: 3.40.4.2, 3.40.4.3, 3.40.4.4, 3.40.4.5,
> and subsections under
> [<u>Section</u>](https://profiles.ihe.net/ITI/TF/Volume2/ITI-20.html#3.20.4)*
>
> *[<u>3.20.4</u>](https://profiles.ihe.net/ITI/TF/Volume2/ITI-20.html#3.20.4)
> (following [<u>Section
> 3.20.4.1.3</u>](https://profiles.ihe.net/ITI/TF/Volume2/ITI-20.html#3.20.4.1.3)
> Expected Actions)*
>
> 665
>
> 670
>
> 675

###  Messages

> <span id="_bookmark32" class="anchor"></span>…

### Send Audit Resource Request Message – FHIR Feed Interaction

> An actor that is grouped with Secure Node or Secure Application, or an
> Audit Record Forwarder, detects an event that should be reported and
> uses the Send Audit Resource Request message to send a report about
> the event to an Audit Record Repository.
>
> A Secure Node, Secure Application or Audit Record Forwarder, that
> supports the ATX: FHIR Feed Option, uses this message to post a single
> AuditEvent Resource to the Audit Record Repository using a FHIR create
> interaction (see
> [<u>https://www.hl7.org/fhir/R4/http.html#create</u>](https://www.hl7.org/fhir/R4/http.html#create)).

### Trigger Events

> This message is sent when an actor that is grouped with Secure Node or
> Secure Application or an Audit Record Forwarder needs to post a single
> AuditEvent Resource to the Audit Record Repository.
>
> There are two trigger events:

1.  A Secure Node or Secure Application detects an event that should be
    reported to the Audit Record Repository. This transaction does not
    specify all of the policies or reasons

> 680
>
> 685
>
> 690
>
> 695
>
> 700
>
> 705
>
> for reporting events. They may be specified in other IHE profiles,
> they may be specified by local law or regulation, or they may be
> specified by local policy.

2.  An Audit Record Forwarder determines that a received AuditEvent
    Resource should be sent to another Audit Record Repository. This
    transaction does not specify what rules or policies determine
    whether an AuditEvent Resource should be forwarded.

> An actor in any IHE profile, when grouped with a Secure Node or Secure
> Application, shall be able to report the events defined in Table
> 3.20.4.1.1.1-1. Additional reportable events are often identified for
> specific events in other IHE profiles, and are documented in that
> profile or transaction.

### Message Semantics

> A Secure Node, Secure Application or Audit Record Forwarder shall
> issue an HTTP request according to requirements defined in the FHIR
> specification for “create” interaction
> ([<u>http://hl7.org/fhir/R4/http.html#create</u>](http://hl7.org/fhir/R4/http.html#create)
> ). The message uses an HTTP POST method to send a FHIR AuditEvent
> Resource.
>
> The Secure Node, Secure Application or Audit Record Forwarder shall
> submit the FHIR AuditEvent Resource in either XML format or JSON
> format. Values for mime-type of the request message are defined in the
> ITI TF-2: Appendix Z.6.
>
> An AuditEvent Resource that reflect Audit Message definition defined
> in IHE Technical Framework shall conform to the requirements defined
> in Section 3.20.4.2.2.1.

### Mapping between DICOM Audit Message definitions and FHIR AuditEvent Resource for the FHIR Feed interactions

> The mappings between IHE defined Audit Message content and FHIR
> AuditEvent Resource is based on FHIR Table 6.4.7.4
> ([<u>http://hl7.org/fhir/R4/auditevent-mappings.html</u>](http://hl7.org/fhir/R4/auditevent-mappings.html))
> that is further constrained in Table 3.20.4.2.2.1-1.
>
> Table 3.20.4.2.2.1-1 is normative and contains mappings from Audit
> Message definitions for IHE transactions and based on DICOM standard
> into a FHIR AuditEvent Resource.
>
> **Table 3.20.4.2.2.1-1: DICOM Audit Message Definitions represented
> into an AuditEvent Resource**

<table style="width:91%;">
<colgroup>
<col style="width: 58%" />
<col style="width: 32%" />
</colgroup>
<thead>
<tr>
<th><blockquote>
<p><strong>DICOM AuditMessage</strong></p>
</blockquote></th>
<th><blockquote>
<p><strong>FHIR AuditEvent Resource</strong></p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr>
<td>EventIdentification.EventID</td>
<td>type</td>
</tr>
<tr>
<td>EventIdentification.EventTypeCode</td>
<td>subtype</td>
</tr>
<tr>
<td>EventIdentification@EventActionCode</td>
<td>action</td>
</tr>
<tr>
<td>EventIdentification@EventDateTime</td>
<td>recorded</td>
</tr>
<tr>
<td>EventIdentification@EventOutcomeIndicator</td>
<td>outcome</td>
</tr>
<tr>
<td>EventIdentification.EventOutcomeDescription</td>
<td>outcomeDesc</td>
</tr>
<tr>
<td>EventIdentification.purposeOfUse</td>
<td>purposeOfEvent</td>
</tr>
<tr>
<td>ActiveParticipant</td>
<td>agent</td>
</tr>
</tbody>
</table>

<table style="width:91%;">
<colgroup>
<col style="width: 58%" />
<col style="width: 32%" />
</colgroup>
<thead>
<tr>
<th><blockquote>
<p><strong>DICOM AuditMessage</strong></p>
</blockquote></th>
<th><blockquote>
<p><strong>FHIR AuditEvent Resource</strong></p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr>
<td>ActiveParticipant.RoleIDCode</td>
<td>agent.type (Note 1)</td>
</tr>
<tr>
<td>ActiveParticipant.RoleIDCode</td>
<td>agent.role (Note 1)</td>
</tr>
<tr>
<td>ActiveParticipant@UserId</td>
<td>agent.who</td>
</tr>
<tr>
<td>ActiveParticipant@AlternativeUserId</td>
<td>agent.altId</td>
</tr>
<tr>
<td>ActiveParticipant@UserName</td>
<td>agent.name</td>
</tr>
<tr>
<td>ActiveParticipant@UserIsRequestor</td>
<td>agent.requestor</td>
</tr>
<tr>
<td>ParticipantRoleIDCode</td>
<td>agent.policy</td>
</tr>
<tr>
<td>ActiveParticipant.MediaIdentifier.MediaType</td>
<td>agent.media</td>
</tr>
<tr>
<td>ActiveParticipant@NetworkAccessPointID</td>
<td>agent.network.address</td>
</tr>
<tr>
<td>ActiveParticipant@NetworkAccessPointTypeCode</td>
<td>agent.network.type</td>
</tr>
<tr>
<td>AuditSourceIdentification</td>
<td>source</td>
</tr>
<tr>
<td>AuditSourceIdentification@AuditEnterpriseSiteId</td>
<td>source.site</td>
</tr>
<tr>
<td>AuditSourceIdentification@AuditSourceId</td>
<td>source.observer</td>
</tr>
<tr>
<td>AuditSourceIdentification.AuditSourcetypeCode</td>
<td>source.type</td>
</tr>
<tr>
<td>ParticipantObjectIdentification</td>
<td>entity</td>
</tr>
<tr>
<td>ParticipantObjectIdentification@ParticipantObjectID and
ParticipantObjectIdentification.ParticipantObjectIDTypeCode</td>
<td>entity.what</td>
</tr>
<tr>
<td>ParticipantObjectIdentification@ParticipantObjectTypeCode</td>
<td>entity.type</td>
</tr>
<tr>
<td>ParticipantObjectIdentification@ParticipantObjectTypeCodeRole</td>
<td>entity.role</td>
</tr>
<tr>
<td>ParticipantObjectIdentification@ParticipantObjectDataLifeCycle</td>
<td>entity.lifecycle</td>
</tr>
<tr>
<td>ParticipantObjectIdentification@ParticipantObjectSensitivity</td>
<td>entity.securityLabel</td>
</tr>
<tr>
<td>ParticipantObjectIdentification.ParticipantObjectName</td>
<td>entity.name (Note 2)</td>
</tr>
<tr>
<td>ParticipantObjectIdentification.ParticipantObjectQuery</td>
<td>entity.query (Note 2)</td>
</tr>
<tr>
<td>ParticipantObjectIdentification.ParticipantObjectDetail</td>
<td>entity.detail</td>
</tr>
<tr>
<td>ParticipantObjectIdentification.ParticipantObjectDetail@type</td>
<td>entity.detail.type</td>
</tr>
<tr>
<td>ParticipantObjectIdentification.ParticipantObjectDetail@value</td>
<td>entity.detail.ValueBase64Binary</td>
</tr>
</tbody>
</table>

> Note 1: If the Audit Record Repository knows the
> ActiveParticipant.RoleIDCode as a type, it should be mapped to
>
> agent.type. Otherwise the default mapping is to agent.role.
>
> 710 Note 2: Only one element between entity.name and entity.query
> shall be used in the AuditEvent Resource

### Expected Actions

> The Audit Record Repository shall support all the mime-types defined
> in ITI TF-2: Appendix Z.6.
>
> 715 On receipt of the Send Audit Resource Request message, the Audit
> Record Repository shall validate the Resources and respond with one of
> the HTTP codes defined in Section 3.20.4.3.2 Message Semantics.
>
> For the Resource received, the Audit Record Repository may:
>
> 720
>
> 725
>
> 730
>
> 735
>
> 740
>
> 745
>
> 750

- discard the Resource as irrelevant

- retain the Resource in an internal data store

- perform other processing on the Resource

> The Audit Record Repository may apply a variety of data retention
> rules to the data store. This transaction does not specify data
> retention rules. These usually depend upon the purposes assigned to a
> specific Audit Record Repository.
>
> If needed, an Audit Record Repository that needs to store a received
> AuditEvent Resource as a DICOM Audit Message can do the transformation
> from the FHIR Resource to a DICOM message according to the
> requirements defined in Table 3.20.4.2.2.1-1.
>
> The Audit Record Repository shall store any resources that were not
> discarded and make them available for further search via the Retrieve
> ATNA Audit Event \[ITI-81\] transaction. These events shall not be
> available for further search via Retrieve Syslog Events \[ITI-82\]
> transaction.
>
> When the Audit Record Repository is grouped with an Audit Record
> Forwarder, the Audit Record Forwarder shall:

- apply filtering rules to all AuditEvent Resources received by the
  Audit Record Repository, and

- forward all AuditEvent Resources that match filters to their
  configured destinations.

> If needed, an Audit Record Forwarder that will forward a received
> AuditEvent Resource using the Audit Event message (DICOM audit event
> via syslog protocol) can do the transformation from the FHIR Resource
> to a DICOM message according to the requirements defined in Table
> <span id="_bookmark37" class="anchor"></span>3.20.4.2.2.1-1.

### Send Audit Resource Response

> The Audit Record Repository responds to the Secure Node, Secure
> Application or Audit Record Forwarder using a Send Audit Resource
> Response message in order to inform the client about the result of the
> operation.

### Trigger Events

> When the Audit Record Repository has finished storing the AuditEvent
> Resource received, it <span id="_bookmark39"
> class="anchor"></span>sends this message back to the client
> acknowledging the result of the request.

### Message Semantics

> The Audit Record Repository returns an HTTP Status code appropriate to
> the processing, conforming to specification requirements as specified
> in
> [<u>https://www.hl7.org/fhir/R4/http.html#create</u>.](https://www.hl7.org/fhir/R4/http.html#create)
>
> If the outcome is a success, the http status code of the response
> shall be a 2xx code.
>
> If the outcome is a failure, the Audit Record Repository shall be
> capable of returning status codes according to what is defined in
> [<u>https://www.hl7.org/fhir/R4/http.html#create</u>](https://www.hl7.org/fhir/R4/http.html#create).
>
> 755
>
> 760
>
> 765
>
> 770
>
> 775
>
> 780
>
> 785
>
> The Audit Record Repository can return other status codes 4xx or 5xx
> in accordance to internal business rules that are out of scope for
> this transaction.

### Expected Actions

> The Audit Record Repository could return failures. For this reason, it
> is up to the client to decide <span id="_bookmark41"
> class="anchor"></span>what to do with failures that have been returned
> by the Audit Record Repository.

### Send Audit Bundle Request Message – FHIR Feed Interaction

> A Secure Node, Secure Application or Audit Record Forwarder that
> supports the ATX: FHIR Feed Option uses this message to post a Bundle
> of AuditEvent Resources to the Audit Record Repository using a FHIR
> batch interaction (see <span id="_bookmark42"
> class="anchor"></span>[<u>https://www.hl7.org/fhir/R4/http.html#transaction</u>](https://www.hl7.org/fhir/R4/http.html#transaction)).

### Trigger Events

> This message is sent when an Audit Record Forwarder or an actor that
> is grouped with Secure Node or Secure Application needs to send
> multiple events that has been audited to the Audit Record Repository.
>
> There are two trigger events:

1.  A Secure Node or Secure Application detects at least one event that
    should be reported to the Audit Record Repository. This transaction
    does not specify all of the policies or reasons for reporting
    events. They may be specified in other IHE profiles, they may be
    specified by local law or regulation, or they may be specified by
    local policy.

2.  An Audit Record Forwarder determines that at least one received
    AuditEvent Resource should be sent to another Audit Record
    Repository. This transaction does not specify what rules or policies
    determine whether an AuditEvent Resource should be forwarded.

> An actor in any IHE profile, when grouped with a Secure Node or Secure
> Application, shall be able to report the events defined in Table
> 3.20.4.1.1.1-1. Additional reportable events are often identified for
> specific events in other IHE profiles, and are documented in that
> profile or <span id="_bookmark43" class="anchor"></span>transaction.

### Message Semantics

> An Audit Record Forwarder or an actor that is grouped with Secure Node
> or Secure Application shall issue an HTTP request according to
> requirements defined in the FHIR specification for “batch” interaction
> (see
> [<u>https://www.hl7.org/fhir/R4/http.html#transaction</u>](https://www.hl7.org/fhir/R4/http.html#transaction)).
>
> The Audit Record Repository and the client shall both support the
> “batch” interaction.
>
> The message uses an HTTP POST method to submit a FHIR Bundle Resource.
> The client shall post FHIR resources in either XML format or JSON
> format. Values for mime-type of the request message are defined in the
> ITI TF-2: Appendix Z.6.
>
> 790
>
> 795
>
> 800
>
> 805
>
> 810
>
> The FHIR Bundle Resource shall contain at least one FHIR AuditEvent
> Resource
> ([<u>https://www.hl7.org/fhir/R4/auditevent.html</u>](https://www.hl7.org/fhir/R4/auditevent.html)).
>
> The element Bundle.entry.request.method shall be POST.
>
> AuditEvent Resources included in the Bundle that reflect Audit Message
> definitions defined in IHE Technical Framework shall conform to the
> requirements defined in Section 3.20.4.2.2.1.

**Table 3.20.4.4.2-1: Bundle Resource Constraints**

<table style="width:93%;">
<colgroup>
<col style="width: 42%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr>
<th style="text-align: center;"><blockquote>
<p><strong>Element &amp;</strong></p>
</blockquote>
<p><strong>Cardinality</strong></p></th>
<th style="text-align: center;"><strong>Constraints</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>type [1..1]</td>
<td>Shall be: batch</td>
</tr>
<tr>
<td>entry [1..*]</td>
<td>Shall contain at least one AuditEvent Resource.</td>
</tr>
<tr>
<td>entry.request.method</td>
<td>Shall be: POST</td>
</tr>
</tbody>
</table>

### Expected Actions

> The Audit Record Repository shall support all the mime-types defined
> in ITI TF-2: Appendix Z.6.
>
> On receipt of the Send Audit Bundle Resource Request, the Audit Record
> Repository shall validate Resources included in it and respond with
> one of the HTTP codes defined in Section
>
> 3.20.4.5.2 Message Semantics.
>
> For each Resource received in the Bundle, the Audit Record Repository
> may:

- Discard the Resource as irrelevant.

- Retain the Resource in an internal data store.

- Perform other processing on the Resource.

> The Audit Record Repository may apply a variety of data retention
> rules to the data store. This transaction does not specify data
> retention rules. These are usually dependent upon the purposes
> assigned to a specific Audit Record Repository.
>
> If needed, an Audit Record Repository that needs to store a received
> AuditEvent Resource as a DICOM Audit Message can do the transformation
> from the FHIR Resource to a DICOM message according to the
> requirements defined in Table 3.20.4.2.2.1-1.
>
> The Audit Record Repository shall store any resources that were not
> discarded and make them available for further search via the Retrieve
> ATNA Audit Event \[ITI-81\] transaction. These events shall not be
> available for further search via Retrieve Syslog Events \[ITI-82\]
> transaction.
>
> 815
>
> 820
>
> 825
>
> 830
>
> 835
>
> 840
>
> 845
>
> When the Audit Record Repository is grouped with an Audit Record
> Forwarder, the Audit Record Forwarder shall:

- Apply filtering rules to all AuditEvent Resources received by the
  Audit Record Repository, and

- Forward all AuditEvent Resources that match filters to their
  configured destinations.

> If needed, an Audit Record Forwarder that needs to forward a received
> AuditEvent Resource using the Audit Event message can do the
> transformation from the FHIR Resource to a DICOM message according to
> the requirements defined in Table 3.20.4.2.2.1-1.

### Send Audit Bundle Response

> The Audit Record Repository sends a Send Audit Bundle Response message
> in response to a Send Audit Bundle Request.

### Trigger Events

> When the Audit Record Repository has finished storing the AuditEvent
> Resources received in the Bundle Resource, it sends back this message
> to the client acknowledging the result of the <span id="_bookmark47"
> class="anchor"></span>request.

### Message Semantics

> The Audit Record Repository returns an HTTP Status code appropriate to
> the processing, conforming to specification requirements as specified
> in
> [<u>https://www.hl7.org/fhir/R4/http.html#transaction-response</u>.](https://www.hl7.org/fhir/R4/http.html#transaction-response)
>
> When the Audit Record Repository has processed the request shall
> return an HTTP response with an overall status code.
>
> To allow the client to know the outcome of the transaction, and the
> identities assigned to the resources by the Audit Record Repository,
> the Audit Record Repository shall return a Bundle, with type set to
> batch-response. Each entry element shall contain a response element
> with an HTTP Status Code which details the outcome of processing of
> the request entry.
>
> If no “Prefer” header is specified in the request the server should
> respond as if it is set to
>
> return=minimal; see
> [<u>https://www.hl7.org/fhir/R4/http.html#ops</u>](https://www.hl7.org/fhir/R4/http.html#ops).
>
> If the outcome of the entry is a success, the http status code of the
> response shall be a 2xx code.
>
> If the outcome of the entry is a failure, the Audit Record Repository
> shall be capable of returning status codes according to what is
> defined in
> [<u>https://www.hl7.org/fhir/R4/http.html#create</u>](https://www.hl7.org/fhir/R4/http.html#create).
>
> The Audit Record Repository can return other status codes 4xx or 5xx
> in accordance to internal business rules that are out of scope for
> this transaction.

### Expected Actions

> The Audit Record Repository could return a partial success for the
> Bundle where some resources succeeded and other not. For this reason,
> it is up to the client to decide what to do with failures that have
> been returned by the Audit Record Repository.
>
> 850
>
> *Editor: Update [<u>Section
> 3.20.5</u>](https://profiles.ihe.net/ITI/TF/Volume2/ITI-20.html#3.20.5)
> as follows*
>
> 855
>
> 860
>
> 865

###  Security Considerations

> The use of the TLS **<u>or HTTPS</u>** transport
> mechanism<img src="./media/image7.png" />is recommended because the
> audit event messages often contain PHI or other sensitive information.
> See [<u>Section
> 3.20.4.1.2.1</u>.](https://profiles.ihe.net/ITI/TF/Volume2/ITI-20.html#3.20.4.1.2.1)
>
> The use of the TLS transport mechanism is not always required because
> there are other means of protection that may be more appropriate in
> some situations. The decision to use the UDP transport mechanism
> should be based upon a security and privacy risk analysis.
>
> The data store within the Audit Record Repository may contain
> sensitive information, and the Audit Record Repository analysis
> facilities may allow sensitive queries. It will be a high value target
> for malicious actors, and should be protected accordingly.
>
> The Audit Record Repository is required to generate audit event
> messages for various kinds of use of the data store and configuration
> changes. This is specified in [<u>Section
> 3.20.4.1.1</u>](https://profiles.ihe.net/ITI/TF/Volume2/ITI-20.html#3.20.4.1.1.1).

### <u>If the AuditEvent Message Option is supported on the Audit Record Repository, update,</u> <u>delete and patch interaction of AuditEvent Resources should be managed by local policies.</u>

### 

> *Editor: Add **new** Sections 3.81 Retrieve ATNA Audit Event and 3.82
> Retrieve Syslog Event to [<u>Volume
> 2</u>.](https://profiles.ihe.net/ITI/TF/Volume2/index.html)*
>
> 870
>
> 875

## Retrieve ATNA Audit Event \[ITI-81\]

> This transaction supports the retrieval of ATNA audit record from the
> Audit Record Repository in accordance with a set of search parameters
> that determine the retrieved event reports. This transaction enables
> an Audit Consumer to search audit events that an Audit Record
> Repository created via the Record Audit Event \[ITI-20\] transaction.
>
> This transaction is a profiling of a standard FHIR search of the
> AuditEvent Resource.

### Scope

> The Retrieve ATNA Audit Event transaction is used to search ATNA
> events recorded in an ATNA Audit Record Repository. The result of this
> retrieval is a FHIR bundle of AuditEvent
>
> 880 Resources that match with a set of search parameters.

### Actor Roles

> **Table 3.81.2-1: Actor Roles**

| **Actor:** | Audit Record Repository |
|----|----|
| **Role:** | Provides storage for ATNA audit events, and responds to queries for a portion of the stored records. |
| **Actor:** | Audit Consumer |
| **Role:** | Queries for ATNA audit records. |

### Referenced Standards

<table style="width:100%;">
<colgroup>
<col style="width: 5%" />
<col style="width: 22%" />
<col style="width: 71%" />
</colgroup>
<thead>
<tr>
<th style="text-align: center;">885</th>
<th><blockquote>
<p>RFC2616</p>
</blockquote></th>
<th>IETF Hypertext Transfer Protocol – HTTP/1.1</th>
</tr>
</thead>
<tbody>
<tr>
<td></td>
<td><blockquote>
<p>RFC4627</p>
</blockquote></td>
<td>The application/json Media Type for JavaScript Object Notation
(JSON)</td>
</tr>
<tr>
<td></td>
<td>RFC6585</td>
<td>IETF Additional HTTP Status Codes</td>
</tr>
<tr>
<td></td>
<td>RFC5424</td>
<td>The Syslog Protocol</td>
</tr>
<tr>
<td></td>
<td>RFC3339</td>
<td>Date and Time on the Internet: Timestamps</td>
</tr>
<tr>
<td style="text-align: center;">890</td>
<td><p>HL7 FHIR</p>
<blockquote>
<p><span id="_bookmark54" class="anchor"></span><strong>3.81.4
Messages</strong></p>
</blockquote></td>
<td>Release 4 <a
href="http://hl7.org/fhir/R4/index.html"><u>http://hl7.org/fhir/R4/index.html</u></a></td>
</tr>
</tbody>
</table>

> Audit Consumer
>
> Audit Record Repository
>
> **Figure 3.81.4-1: Interaction Diagram**
>
> 895
>
> 900
>
> 905
>
> 910
>
> 915
>
> 920
>
> 925

###  Retrieve ATNA Audit Events Message

> This is an HTTP GET parameterized search from an Audit Consumer to an
> Audit Record Repository. The Audit Record Repository has stored ATNA
> audit records received via Record Audit Event \[ITI-20\] transactions.
> Those messages, which are stored within a data-store, can be retrieved
> in accordance with specific search parameters.

### Trigger Events

> The Audit Consumer sends a Retrieve ATNA Audit Events message when it
> needs to process or <span id="_bookmark57"
> class="anchor"></span>analyze ATNA audit records.

### Message Semantics

> The Retrieve ATNA Audit Event message shall be an HTTP GET request
> sent to the Audit Record Repository. This message is a FHIR search
> (see
> [<u>http://hl7.org/fhir/R4/search.html</u>](http://hl7.org/fhir/R4/search.html))
> on AuditEvent Resources (see
> [<u>http://hl7.org/fhir/R4/auditevent.html</u>](http://hl7.org/fhir/R4/auditevent.html)).
> This “search” target is formatted as:
>
> \<scheme\>://\<authority\>/\<path\>/AuditEvent?date=ge\[start-time\]&date=le\[stop-time\]&\<query\>
>
> where:

- \<scheme\> shall be either http or https. The use of http or https is
  a policy decision, but https is usually appropriate due to
  confidentiality of ATNA audit record content;

- \<authority\> shall be represented as a host (either IP address or DNS
  name) followed optionally by a colon and port number.

- The Audit Record Repository may use \<path\> to segregate the HTTP
  search service for AuditEvent implementation from other REST-based
  services.

- At least one date search parameter is required. See Section
  3.81.4.1.2.1.

- **“&”** is a conditional parameter that shall be present if the
  \<query\> parameter is present.

- \<query\>, if present, represents a series of encoded name-value pairs
  representing filters <span id="_bookmark58" class="anchor"></span>for
  the search. See Section 3.81.4.1.2.2.

### Date Search Parameters

> The date parameter shall be used to specify an upper and/or lower
> bound for the search. At least one date parameter shall be present.
> Two date parameters are recommended in every search by the Audit
> Consumer and shall be supported by the Audit Record Repository in
> order to avoid overloading the Audit Consumer. These parameters allow
> the Audit Consumer to specify the time frame of creation of audit
> records of interest and enable the Audit Consumer to constrain
>
> the number of audit records returned. The values for the date search
> parameters shall be in RFC3339 format.
>
> Note: RFC3339 format is the format mandated by Syslog for time stamps
> and is a sub-set of the XML date-time data format used by FHIR.
>
> 930 For example, to search AuditEvent Resources created during the
> whole day of January 5, 2013:
>
> <http://example.com/ARRservice/AuditEvent?date=ge2013-01-05&date=le2013-01-05>
>
> 935
>
> 940
>
> 945
>
> 950
>
> 955
>
> The Audit Record Repository shall apply matching criteria to
> AuditEvent Resources characterized by AuditEvent.recorded field valued
> within the time frame specified in the Request message.
>
> The Audit Record Repository shall apply other date matching criteria
> following rules defined by <span id="_bookmark59"
> class="anchor"></span>FHIR specification
> ([<u>http://hl7.org/fhir/R4/search.html</u>](http://hl7.org/fhir/R4/search.html)).

### Additional ATNA Search Parameters

> The search parameters in this section may be supported by the Audit
> Consumer and shall be supported by the Audit Record Repository. These
> parameters can be used by the Audit Consumer to refine search
> requests. Refer to Section 3.81.4.2.2 for the mapping between the FHIR
> AuditEvent Resource and the DICOM standard definition.
>
> The Audit Consumer shall encode all search parameters per RFC3986
> “percent” encoding rules. Although FHIR allows unconstrained use of
> AND OR operators to make queries of unlimited complexity, this
> transaction constrains the queries allowed:

- Multiple search parameters shall only be combined using AND **“&”**
  operator.

- The OR **“,”** operator shall be used only within a single search
  parameter that has multiple values.

> Additional search parameters are listed below:

- address is a parameter of string type. This parameter specifies the
  identifier of the network access point (NetworkAccessPointID) of the
  user device that creates the audit record (this could be a device id,
  IP address, or some other identifier associated with a device).

> The value of this parameter shall contain the substring to match.
>
> 960
>
> For example:
>
> <http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013->01-02&address=192.168.0.1
>
> The Audit Record Repository shall match this parameter with the
>
> AuditEvent.agent.network.address.

- agent.identifier is a parameter of token type. This parameter
  identifies the user that participated in the event that originates the
  audit record.

> 965 For example, to search AuditEvent Resources related to the user
> “admin”:
>
> <http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013->01-02&agent.identifier=admin
>
> 970
>
> 975
>
> 980
>
> The Audit Record Repository shall match this parameter with the
>
> AuditEvent.agent.who.identifier field.
>
> If a patient identifier it is used, the Audit Record Repository will
> return only the audit records where the patient is involved in the
> event as a user.

- patient.identifier is a parameter of token type. This parameter
  specifies the identifier of the patient involved in the event as a
  participant or as a user. The value of this parameter can contain the
  namespace URI (that represents the assigning authority for the
  identifier) and the identifier.

> For example:
>
> <http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013->01-02&patient.identifier=urn:oid:1.2.3.4\|5678
>
> 985
>
> 990
>
> The Audit Record Repository shall match this parameter with the
> AuditEvent.agent.who.identifier and AuditEvent.entity.what.identifier
> where the reference resolve to a Patient.

- entity.identifier is a parameter of token type. This parameter
  specifies unique identifier for the object. The parameter value should
  be identified in accordance to the entity type.

> For example:

- ?entity.identifier=urn:oid:1.2.3.4.5\|123-203-FJ

- ?entity.identifier=\|123-203-FJ.

> 995
>
> 1000
>
> The Audit Record Repository shall match this parameter with the
> AuditEvent.entity.what.identifier field that is of type identifier
> (ParticipantObjectID in DICOM schema). If a patient identifier is used
> the Audit Record Repository will return only audit records where the
> patient is involved in the event as a participant.

- entity-type is a parameter of token type. This parameter specifies the
  type of the object (e.g., Person, System Object, etc.). The parameter
  value shall contain the CodeSystem namespace URI
  <http://terminology.hl7.org/CodeSystem/audit-entity-type> or
  <http://hl7.org/fhir/resource-types> defined by FHIR and a coded
  value. See
  [<u>http://hl7.org/fhir/R4/valueset-audit-entity-type.html</u>](http://hl7.org/fhir/R4/valueset-audit-entity-type.html)
  for codes that shall be used.

> 1005
>
> 1010
>
> 1015
>
> 1020
>
> The Audit Record Repository shall match this parameter with the
>
> AuditEvent.entity.type field.

- entity-role is a parameter of token type. This parameter specifies the
  role played by the entity (e.g., Report, Location, Query, etc.). The
  parameter value shall contain the namespace URI
  <http://hl7.org/fhir/object-role> defined by FHIR and a coded value.
  See
  [<u>http://hl7.org/fhir/R4/object-role</u>](http://hl7.org/fhir/R4/object-role)
  for codes that shall be used.

> For example, to search all the audit records related to the document
> entity (Report=”3”) with the unique id 12345^1.2.3.4.5 a fully
> specified request would be:
>
> <http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013->01-02&entity-role=<http://hl7.org/fhir/object-role>\|3&entity-id=urn:oid:1.2.3.4.5\|12345
>
> The Audit Record Repository shall match this parameter with the
>
> AuditEvent.entity.role field.

- source.identifier is a parameter of token type. This parameter
  identifies the source of the audit event (DICOM AuditSourceID).

> For example, to search AuditEvent Resources produced by the audit
> source application characterized by unique ID: 1234:
>
> <http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013->01-02&source=1234
>
> 1025
>
> 1030
>
> 1035
>
> The Audit Record Repository shall match this parameter with the
>
> AuditEvent.source.observer.identifier field.

- type is a parameter of token type. This parameter represents the
  identifier of the specific type of event audited. The parameter value
  shall contain the namespace URI
  <http://dicom.nema.org/resources/ontology/DCM> and a coded value.
  Codes available are defined by DICOM and IHE (see ITI TF-1: Table
  3.20.4.1.1.1-1: Audit Record trigger events).

> For example, to search AuditEvent Resources related to PHI Export
> Events:
>
> <http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013->01-02&type=<http://dicom.nema.org/resources/ontology/DCM>\|110106
>
> 1040
>
> The Audit Record Repository shall match this parameter with the
> AuditEvent.type field (DICOM EventID).

- subtype is parameter of token type. This parameter identifies the
  specific IHE transaction that originates the audit record. The
  parameter value can contain the namespace URI urn:ihe:event-type-code
  to search for audit messages triggered by IHE transactions with the
  defined audit message. Each IHE transaction that defines an

> 1045
>
> 1050
>
> 1055
>
> ATNA messages, specifies a code identifying the transaction itself,
> and assigns this code to the EventTypeCode element within the
> \[ITI-20\] audit record.
>
> For example, to search AuditEvent Resources related to [<u>Retrieve
> Document Set
> \[ITI-43\]</u>](https://profiles.ihe.net/ITI/TF/Volume2/ITI-43.html)
> transactions:
>
> <http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013->01-02&subtype=urn:ihe:event-type-code\|ITI-43
>
> The Audit Record Repository shall match this parameter with the
> AuditEvent.subtype
>
> field (DICOM EventTypeCode).

- outcome is a parameter of token type. This parameter represents
  whether the event succeeded or failed. The parameter value shall
  contain the namespace URI <http://hl7.org/fhir/audit-event-outcome>
  and a code taken from the related value set. See
  [<u>http://hl7.org/fhir/R4/valueset-audit-event-outcome.html</u>](http://hl7.org/fhir/R4/valueset-audit-event-outcome.html).

> 1060
>
> 1065
>
> 1070
>
> 1075
>
> 1080
>
> To search AuditEvent Resources related to failed events:
>
> <http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013->01-02&outcome=<http://hl7.org/fhir/audit-event-outcome>\|4,8,12
>
> The Audit Record Repository shall match this parameter with the
> AuditEvent.outcome
>
> field (DICOM EventOutcomeIndicator).
>
> The HL7<sup>®</sup> FHIR<sup>®</sup> standard provides additional
> search parameters. This transaction does not define specific behavior
> on those parameters (such as \_sort, \_include, etc.). See
> [<u>http://hl7.org/fhir/R4/search.html</u>](http://hl7.org/fhir/R4/search.html)
> for details about available parameters.

### Populating Expected Response Format

> The HL7<sup>®</sup> FHIR<sup>®</sup> standard provides encodings for
> responses as either XML or JSON. The Audit Record Repository shall
> support both message encodings. The Audit Consumer shall support one
> and may optionally support both encodings. For Desired Response
> Encoding and format negotiation see ITI TF-2: Appendix Z.6.

### Expected Actions

> The Audit Record Repository (ARR) maintains a database of audit
> events. The Audit Record Repository retains data according to local
> policies, and some data may be deleted.
>
> The Audit Record Repository shall return all the audit events stored
> in its database that match the query parameters, and which the
> requester is authorized to view (see [<u>ITI TF-1:
> 9.4</u>](https://profiles.ihe.net/ITI/TF/Volume1/ch-9.html#9.4) for
> further details).
>
> When performing matching based on the search parameters, the Audit
> Record Repository shall:
>
> 1085
>
> 1090
>
> 1095
>
> 1100
>
> 1105
>
> 1110

- Select all audit records that have a time interval specified in the
  request URL.

- If search parameters other than those defined in Section 3.81.4.1.2.2
  (e.g., \_sort,

> \_include FHIR search result parameters) are specified in the request
> URL, then

- If the Audit Record Repository does not support the parameter, it
  shall be ignored;

- If the Audit Record Repository supports the parameter, the matching or
  other behavior shall comply with the matching rules for its datatype
  in FHIR.

> The Audit Record Repository shall return matching resources using the
> Retrieve ATNA Audit <span id="_bookmark62" class="anchor"></span>Event
> Response Message. See Section 3.81.4.2.

### Retrieve ATNA Audit Event Response Message

> The Audit Record Repository sends the Retrieve ATNA Audit Event
> Response message in response to a query from an Audit Consumer

### Trigger Events

> The Audit Record Repository creates this message when it receives and
> processes a Retrieve <span id="_bookmark64" class="anchor"></span>ATNA
> Audit Event message.

### Message Semantics

> When the Audit Record Repository successfully processes the search
> request, it shall return the matching AuditEvent Resources inside a
> FHIR Bundle Resource.
>
> The “Content-Type” of the response will depend upon the response
> format negotiation described in ITI TF-2: Appendix Z.6.
>
> If the date search parameter is missing (see Section 3.81.4.1.2.1),
> the Audit Record Repository may return HTTP response code 400 - Bad
> Request.
>
> If the specified search parameters do not result in any matching audit
> record, the Audit Record Repository shall return HTTP response of
> success 200, with an empty FHIR bundle.
>
> If the requested data size is considered excessive by the Audit Record
> Repository, it may choose to return the results in a series of pages
> (see
> [<u>https://www.hl7.org/fhir/R4/http.html#paging</u>](https://www.hl7.org/fhir/R4/http.html#paging)).
>
> Other HTTP response codes may be returned by the Audit Record
> Repository, indicating conditions outside of the scope of this
> transaction, for example, 401 – Authentication Failed might be
> returned if Audit Record Repository is grouped with the Kerberized
> Server in the EUA Profile. See ITI TF-2: Appendix Z.7 “Guidance on
> Access Denied Results”.
>
> The Audit Record Repository should complement the returned error code
> with a human readable description of the error condition.
>
> Audit Record Repository may return HTTP redirect responses (responses
> with values of 301, 302, 303, or 307) in response to a request. Audit
> Consumers must follow redirects, but if a loop is detected, it may
> report an error.
>
> 1115
>
> 1120
>
> 1125

###  Mapping between FHIR and DICOM for query interaction

> The mapping rules between FHIR AuditEvent Resources and DICOM
> AuditMessage format is based on FHIR Table 6.4.7.4
> ([<u>http://hl7.org/fhir/R4/auditevent-mappings.html</u>](http://hl7.org/fhir/R4/auditevent-mappings.html))
> that is further constrained in Table 3.81.4.2.2.1-1.
>
> Table 3.81.4.2.2.1-1 is normative and defined a strict alignment
> between the AuditEvent Resource and the DICOM AuditMessage. However,
> Table 3.81.4.2.2.1-1 does not aim to resolve the dissonance between
> the FHIR AuditEvent Resource and the DICOM AuditMessage, but rather it
> ensures interoperability between these two data models.
>
> The Audit Record Repository shall encode all the data within the DICOM
> format of the AuditMessage into the AuditEvent Resource(s) sent in the
> Retrieve ATNA Audit Event Response message.
>
> **Table 3.81.4.2.2.1-1: DICOM Tag Mapping for query interaction**

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 66%" />
</colgroup>
<thead>
<tr>
<th><blockquote>
<p><strong>AuditEvent Resource</strong></p>
</blockquote></th>
<th style="text-align: center;"><strong>AuditMessage</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>type</td>
<td>EventIdentification.EventID</td>
</tr>
<tr>
<td>subtype</td>
<td>EventIdentification.EventTypeCode</td>
</tr>
<tr>
<td>action</td>
<td>EventIdentification@EventActionCode</td>
</tr>
<tr>
<td>period</td>
<td>NOT PRESENT</td>
</tr>
<tr>
<td>recorded</td>
<td>EventIdentification@EventDateTime</td>
</tr>
<tr>
<td>outcome</td>
<td>EventIdentification@EventOutcomeIndicator</td>
</tr>
<tr>
<td>outcomeDesc</td>
<td>EventIdentification.EventOutcomeDescription</td>
</tr>
<tr>
<td>purposeOfEvent</td>
<td>EventIdentification.purposeOfUse</td>
</tr>
<tr>
<td>agent</td>
<td>ActiveParticipant</td>
</tr>
<tr>
<td>agent.type (Note 1)</td>
<td>ActiveParticipant.RoleIDCode</td>
</tr>
<tr>
<td>agent.role (Note 1)</td>
<td>ActiveParticipant.RoleIDCode</td>
</tr>
<tr>
<td>agent.who</td>
<td>ActiveParticipant@UserId</td>
</tr>
<tr>
<td>agent.altId</td>
<td>ActiveParticipant@AlternativeUserId</td>
</tr>
<tr>
<td>agent.name</td>
<td>ActiveParticipant@UserName</td>
</tr>
<tr>
<td>agent.requestor</td>
<td>ActiveParticipant@UserIsRequestor</td>
</tr>
<tr>
<td>agent.location</td>
<td>NOT PRESENT</td>
</tr>
<tr>
<td>agent.policy</td>
<td>ParticipantRoleIDCode</td>
</tr>
<tr>
<td>agent.media</td>
<td>ActiveParticipant.MediaIdentifier.MediaType</td>
</tr>
<tr>
<td>agent.network.address</td>
<td>ActiveParticipant@NetworkAccessPointID</td>
</tr>
<tr>
<td>agent.network.type</td>
<td>ActiveParticipant@NetworkAccessPointTypeCode</td>
</tr>
<tr>
<td>agent.purposeOfUse</td>
<td>NOT PRESENT</td>
</tr>
<tr>
<td>source</td>
<td>AuditSourceIdentification</td>
</tr>
<tr>
<td>source.site</td>
<td>AuditSourceIdentification@AuditEnterpriseSiteId</td>
</tr>
<tr>
<td>source.observer</td>
<td>AuditSourceIdentification@AuditSourceId</td>
</tr>
<tr>
<td>source.type</td>
<td>AuditSourceIdentification.AuditSourcetypeCode</td>
</tr>
<tr>
<td>entity</td>
<td>ParticipantObjectIdentification</td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 66%" />
</colgroup>
<thead>
<tr>
<th><blockquote>
<p><strong>AuditEvent Resource</strong></p>
</blockquote></th>
<th style="text-align: center;"><strong>AuditMessage</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>entity.what</td>
<td>ParticipantObjectIdentification@ParticipantObjectID and
ParticipantObjectIdentification.ParticipantObjectIDTypeCode</td>
</tr>
<tr>
<td>entity.type</td>
<td>ParticipantObjectIdentification@ParticipantObjectTypeCode</td>
</tr>
<tr>
<td>entity.role</td>
<td>ParticipantObjectIdentification@ParticipantObjectTypeCodeRole</td>
</tr>
<tr>
<td>entity.lifecycle</td>
<td>ParticipantObjectIdentification@ParticipantObjectDataLifeCycle</td>
</tr>
<tr>
<td>entity.securityLabel</td>
<td>ParticipantObjectIdentification@ParticipantObjectSensitivity</td>
</tr>
<tr>
<td>entity.name</td>
<td>ParticipantObjectIdentification.ParticipantObjectName</td>
</tr>
<tr>
<td>entity.description</td>
<td>NOT PRESENT</td>
</tr>
<tr>
<td>entity.query</td>
<td>ParticipantObjectIdentification.ParticipantObjectQuery</td>
</tr>
<tr>
<td>entity.detail</td>
<td>ParticipantObjectIdentification.ParticipantObjectDetail</td>
</tr>
<tr>
<td>entity.detail.type</td>
<td>ParticipantObjectIdentification.ParticipantObjectDetail@type</td>
</tr>
<tr>
<td>entity.detail.ValueBase64Binary</td>
<td>ParticipantObjectIdentification.ParticipantObjectDetail@value</td>
</tr>
</tbody>
</table>

> 1130
>
> Note 1: If the Audit Record Repository knows the
> ActiveParticipant.RoleIDCode as a type, it should be mapped to
>
> agent.type. Otherwise the default mapping is to agent.role.
>
> Note 2: Values recorded in the
> ParticipantObjectIdentification.ParticipantObjectDescription element
> shall be represented in the extension defined in
> [https://www.hl7.org/fhir/R4/auditevent-profiles.html -
> extensions](https://www.hl7.org/fhir/R4/auditevent-profiles.html#extensions)
> .
>
> 1135

###  FHIR Bundle of Audit Events Messages

> When the search is successful, the body of the Response message shall
> contain a FHIR Bundle of AuditEvent Resources.
>
> Example XML format:
>
> \<Bundle\>
>
> \<type\>searchset\</type\>
>
> \<total\>3\</total\>
>
> \<link\>
>
> \<relation value=”self”/\>
>
> \<url value=”
> [http://example.com/ARRservice/AuditEvent?date=&gt;2013-01-01&date=&lt;2013-](http://example.com/ARRservice/AuditEvent?date&gt%3B2013-01-01&date&lt%3B2013-)01-02”/\>
>
> \</link\>
>
> \<entry\>
>
> \<fullUrl
> value=["http://example.com/ARRservice/AuditEvent/23#"](http://example.com/ARRservice/AuditEvent/23)/\>
>
> \<resource\>

\<AuditEvent\>

.....

\</AuditEvent\>

\<resource\>

> \</entry\>

\<entry\>

> \<fullUrl
> value=["http://example.com/ARRservice/AuditEvent/564#"](http://example.com/ARRservice/AuditEvent/564)/\>
>
> \<resource\>

\<AuditEvent\>

.....

\</AuditEvent\>

\<resource\>

> \</entry\>

\<entry\>

> \<fullUrl
> value=["http://example.com/ARRservice/AuditEvent/3446#"](http://example.com/ARRservice/AuditEvent/3446)/\>
>
> \<resource\>

\<AuditEvent\>

.....

\</AuditEvent\>

\<resource\>

> \</entry\>

\</Bundle\>

> 1145
>
> 1150
>
> 1155
>
> 1160
>
> 1165
>
> 1170
>
> 1175
>
> 1180

###  Expected Actions

> The Audit Consumer may further analyze the data received within the
> FHIR Bundle of AuditEvent Resources.

### Security Considerations

> <span id="_bookmark69" class="anchor"></span>See the general Security
> Considerations in [<u>ITI TF-1:
> 9.5</u>.](https://profiles.ihe.net/ITI/TF/Volume1/ch-9.html#9.5)

### Security Audit Considerations

> This transaction may involve the disclosure of sensitive information.
> Logging these retrieval transactions as a query event is appropriate.
> However, ATNA Profile does not require the Audit Record Repository to
> be able to send audit records using the Record Audit Event \[ITI-20\]
> transaction. The Audit Record Repository shall create and store
> locally an audit event as follows:

<table style="width:100%;">
<colgroup>
<col style="width: 15%" />
<col style="width: 29%" />
<col style="width: 7%" />
<col style="width: 47%" />
</colgroup>
<thead>
<tr>
<th style="text-align: center;"></th>
<th><blockquote>
<p><strong>Field Name</strong></p>
</blockquote></th>
<th style="text-align: center;"><strong>Opt</strong></th>
<th><blockquote>
<p><strong>Value Constraints</strong></p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="3"
style="text-align: center;"><p><strong>Event</strong></p>
<blockquote>
<p>AuditMessage/ EventIdentification</p>
</blockquote></td>
<td><blockquote>
<p>EventID</p>
</blockquote></td>
<td style="text-align: center;">M</td>
<td>EV <a
href="http://dicom.nema.org/medical/dicom/current/output/chtml/part16/chapter_D.html#DCM_110101">(110101,
DCM, "Audit Log Used")</a></td>
</tr>
<tr>
<td><blockquote>
<p>EventActionCode</p>
</blockquote></td>
<td style="text-align: center;">M</td>
<td>“R” (Read)</td>
</tr>
<tr>
<td><blockquote>
<p><em>EventDateTime</em></p>
</blockquote></td>
<td style="text-align: center;"><em>U</em></td>
<td><em>not specialized</em></td>
</tr>
</tbody>
</table>

<table style="width:100%;">
<colgroup>
<col style="width: 15%" />
<col style="width: 29%" />
<col style="width: 7%" />
<col style="width: 47%" />
</colgroup>
<thead>
<tr>
<th rowspan="2"></th>
<th><blockquote>
<p><em>EventOutcomeIndicator</em></p>
</blockquote></th>
<th style="text-align: center;"><em>U</em></th>
<th><em>not specialized</em></th>
</tr>
<tr>
<th><blockquote>
<p>EventTypeCode</p>
</blockquote></th>
<th style="text-align: center;">M</th>
<th>EV(“ITI-81”, “IHE Transactions”, “Retrieve ATNA AuditEvent”)</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="4">Source (Document Administrator) (1)</td>
</tr>
<tr>
<td colspan="4">Human Requestor (0..1)</td>
</tr>
<tr>
<td colspan="4">Destination (Document Registry) (1)</td>
</tr>
<tr>
<td colspan="4">Audit Source (Document Administrator) (1)</td>
</tr>
<tr>
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
<tr>
<th><blockquote>
<p><strong>Source</strong></p>
</blockquote></th>
<th><em>UserID</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="6"><blockquote>
<p>AuditMessage/ ActiveParticipant</p>
</blockquote></td>
<td>AlternativeUserID</td>
<td style="text-align: center;">M</td>
<td><blockquote>
<p>The process ID as used within the local operating system in the local
system logs.</p>
</blockquote></td>
</tr>
<tr>
<td><em>UserName</em></td>
<td style="text-align: center;"><em>U</em></td>
<td><blockquote>
<p><em>not specialized</em></p>
</blockquote></td>
</tr>
<tr>
<td><em>UserIsRequestor</em></td>
<td style="text-align: center;"><em>U</em></td>
<td><blockquote>
<p><em>not specialized</em></p>
</blockquote></td>
</tr>
<tr>
<td>RoleIDCode</td>
<td style="text-align: center;">M</td>
<td><blockquote>
<p>EV(110153, DCM, “Source Role ID”)</p>
</blockquote></td>
</tr>
<tr>
<td>NetworkAccessPointTypeCode</td>
<td style="text-align: center;">M</td>
<td><blockquote>
<p>“1” for machine (DNS) name, “2” for IP address</p>
</blockquote></td>
</tr>
<tr>
<td>NetworkAccessPointID</td>
<td style="text-align: center;">M</td>
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
<tr>
<th rowspan="7" style="text-align: center;"><blockquote>
<p><strong>Human Requestor (if known)</strong></p>
<p>AuditMessage/ ActiveParticipant</p>
</blockquote></th>
<th>UserID</th>
<th style="text-align: center;">M</th>
<th><blockquote>
<p>Identity of the human that initiated the transaction.</p>
</blockquote></th>
</tr>
<tr>
<th><em>AlternativeUserID</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr>
<th><em>UserName</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr>
<th><em>UserIsRequestor</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr>
<th>RoleIDCode</th>
<th style="text-align: center;">M</th>
<th><blockquote>
<p>Access Control role(s) the user holds that allows this
transaction.</p>
</blockquote></th>
</tr>
<tr>
<th><em>NetworkAccessPointTypeCode</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr>
<th><em>NetworkAccessPointID</em></th>
<th style="text-align: center;"><em>U</em></th>
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
<tr>
<th><blockquote>
<p><strong>Destination</strong></p>
</blockquote></th>
<th>UserID</th>
<th style="text-align: center;">M</th>
<th><blockquote>
<p>SOAP endpoint URI.</p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="6"><blockquote>
<p>AuditMessage/ ActiveParticipant</p>
</blockquote></td>
<td><em>AlternativeUserID</em></td>
<td style="text-align: center;"><em>U</em></td>
<td><blockquote>
<p><em>not specialized</em></p>
</blockquote></td>
</tr>
<tr>
<td><em>UserName</em></td>
<td style="text-align: center;"><em>U</em></td>
<td><blockquote>
<p><em>not specialized</em></p>
</blockquote></td>
</tr>
<tr>
<td><em>UserIsRequestor</em></td>
<td style="text-align: center;"><em>U</em></td>
<td><blockquote>
<p><em>not specialized</em></p>
</blockquote></td>
</tr>
<tr>
<td>RoleIDCode</td>
<td style="text-align: center;">M</td>
<td><blockquote>
<p>EV(110152, DCM, “Destination Role ID”)</p>
</blockquote></td>
</tr>
<tr>
<td>NetworkAccessPointTypeCode</td>
<td style="text-align: center;">M</td>
<td><blockquote>
<p>“1” for machine (DNS) name, “2” for IP address</p>
</blockquote></td>
</tr>
<tr>
<td>NetworkAccessPointID</td>
<td style="text-align: center;">M</td>
<td><blockquote>
<p>The machine name or IP address.</p>
</blockquote></td>
</tr>
</tbody>
</table>

> 1185

<table>
<colgroup>
<col style="width: 16%" />
<col style="width: 29%" />
<col style="width: 6%" />
<col style="width: 47%" />
</colgroup>
<thead>
<tr>
<th rowspan="3" style="text-align: center;"><blockquote>
<p><strong>Audit Source</strong></p>
</blockquote>
<p>AuditMessage/AuditSou rceIdentification</p></th>
<th><em>AuditSourceID</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><em>not specialized</em></th>
</tr>
<tr>
<th><em>AuditEnterpriseSiteID</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><em>not specialized</em></th>
</tr>
<tr>
<th><em>AuditSourceTypeCode</em></th>
<th style="text-align: center;"><em>U</em></th>
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
<tr>
<th rowspan="9" style="text-align: center;"><blockquote>
<p><strong>AuditEvent Message</strong></p>
<p>AuditMessage/ ParticipantObjectIdentif ication</p>
</blockquote></th>
<th>ParticipantObjectTypeCode</th>
<th style="text-align: center;">M</th>
<th><blockquote>
<p>“2” (System object)</p>
</blockquote></th>
</tr>
<tr>
<th>ParticipantObjectTypeCodeRole</th>
<th style="text-align: center;">M</th>
<th><blockquote>
<p>“13” (Security Resource)</p>
</blockquote></th>
</tr>
<tr>
<th><em>ParticipantObjectDataLifeCycle</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr>
<th>ParticipantObjectIDTypeCode</th>
<th style="text-align: center;">M</th>
<th><blockquote>
<p>EV(“12”, “RFC-3881”, "URI")</p>
</blockquote></th>
</tr>
<tr>
<th><em>ParticipantObjectSensitivity</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr>
<th>ParticipantObjectID</th>
<th style="text-align: center;">M</th>
<th><blockquote>
<p>The URI of the Audit log</p>
</blockquote></th>
</tr>
<tr>
<th>ParticipantObjectName</th>
<th style="text-align: center;">U</th>
<th><blockquote>
<p>“Security Audit Log”</p>
</blockquote></th>
</tr>
<tr>
<th><em>ParticipantObjectQuery</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr>
<th><em>ParticipantObjectDetail</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

> 1190
>
> 1195
>
> 1200

##  Retrieve Syslog Event

> This transaction supports the retrieval of syslog messages from the
> Audit Record Repository subject to parameters that limit the
> retrieval.

### Scope

> The Retrieve Syslog Event transaction is used to search events
> recorded.

### Use-case Roles

> **Actor:** Audit Record Repository
>
> **Role:** Provides storage for syslog messages, and responds to
> queries for a portion of the stored messages.
>
> **Actor:** Audit Consumer
>
> <span id="_bookmark73" class="anchor"></span>**Role:** Queries for
> audit records.

### Referenced Standards

> RFC2616 IETF Hypertext Transfer Protocol – HTTP/1.1
>
> RFC4627 The application/json Media Type for JavaScript Object Notation
> (JSON)
>
> 1205
>
> RFC6585 IETF Additional HTTP Status Codes RFC5424 The Syslog Protocol
>
> RFC3339 Date and Time on the Internet: Timestamps

### Messages

### 

> Audit Consumer Audit Record Repository
>
> **Figure 3.82.4-1: Interaction Diagram**
>
> 1210
>
> 1215
>
> 1220
>
> 1225

###  Retrieve Syslog Event Request Message

> This message shall be an HTTP GET parameterized search from an Audit
> Consumer to an Audit Record Repository. The Audit Record Repository
> maintains a database of received syslog messages. This database may be
> a subset of all messages received and it may include messages that do
> not adhere to the IHE Audit Trail format defined in the Record Audit
> Event \[ITI-20\] transaction. See [<u>ITI TF-2:
> 3.20.7</u>](https://profiles.ihe.net/ITI/TF/Volume2/ITI-20.html#3.20.7)
> Audit Message Format. The Audit Record Repository may have selection
> criteria for what kinds of messages are kept for later search, how
> long different kinds of messages are kept, etc.

### Trigger Events

> <span id="_bookmark77" class="anchor"></span>This message is sent when
> the Audit Consumer needs syslog messages to process.

### Message Semantics

> The Retrieve Syslog Event Request message is an HTTP GET request sent
> by the Audit Consumer to the Retrieve Syslog Event URL on the Audit
> Record Repository. The “search” target is formatted as:
>
> \<scheme\>://\<authority\>/\<path\>/syslogsearch?date=le\[start-time\]&date=ge\[stop-time\]&\<query\>
>
> Where:

- \<scheme\> shall be either http or https. The use of http or https is
  a policy decision, but https is usually appropriate due to
  confidentiality of syslog message content;

> 1230
>
> 1235
>
> 1240
>
> 1245
>
> 1250
>
> 1255
>
> 1260

- \<authority\> shall be represented as a host (either IP address or DNS
  name) followed optionally by a colon and port number.

- The Audit Record Repository may use \<path\> to segregate the search
  from other services.

- “syslogsearch” is a required part of the URL that allows the Audit
  Consumer to ask for syslog messages stored in the Audit Record
  Repository.

- At least one date search parameters id required. See Section
  3.82.4.1.2.1.

- **“&”** is a conditional parameter that shall be present if the
  \<query\> parameter is present.

- \<query\>, if present, represents additional search parameters. See
  Section 3.82.4.1.2.2.

> The Audit Consumer may indicate the preferred format of the response
> in the HTTP “Accept” header.

### Date Search Parameters

> One or two **date** parameters shall be present in every search by the
> Audit Consumer and shall be supported by the Audit Record Repository.
> Using two parameters allows the Audit Consumer to specify the time
> frame of creation of syslog messages of interest and enable the Audit
> Consumer to constrain the number of syslog messages returned. The
> lower and upper bound for time shall be in RFC3339 format.
>
> Note: RFC3339 format is the format mandated by Syslog for time stamps
> and is a sub-set of the XML date-time data format.
>
> To search syslog messages created during the whole day of January 5,
> 2013, the search URL is:
>
> <http://example.com/ARRservice/syslogsearch?date=ge2013-01-05&date=le2013-01->05
>
> This parameter matches with the time of the syslog message creation.

### Additional Search Parameters

> The search parameters in this section may be supported by the Audit
> Consumer and shall be supported by the Audit Record Repository. These
> parameters can be used by the Audit Consumer to refine search
> requests.
>
> The Audit Consumer may include additional search parameters. These
> search parameters shall be encoded in accordance with RFC3986 for
> encoding GET queries.
>
> The search string is encoded as a list of search parameter/value
> pairs, using the parameter names in column 2 of Table 3.82.4.1.2.2-1
> to indicate the syslog message element being matched. There is a
> search parameter assigned for each syslog metadata element. In all
> cases:

- The search values shall be encoded as strings.

- The syslog message is considered to match if the value string is a
  sub-string found in the specified message element.

> 1265
>
> 1270
>
> 1275
>
> 1280
>
> 1285
>
> 1290
>
> **Table 3.82.4.1.2.2-1: Retrieve Syslog Event search parameters
> mapping with syslog metadata**

<table style="width:64%;">
<colgroup>
<col style="width: 30%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr>
<th><blockquote>
<p><strong>Syslog RFC5424 element</strong></p>
</blockquote></th>
<th><blockquote>
<p><strong>Retrieve Syslog Event Search Parameter</strong></p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr>
<td>PRI</td>
<td>pri</td>
</tr>
<tr>
<td>VERSION</td>
<td>version</td>
</tr>
<tr>
<td>HOSTNAME</td>
<td>hostname</td>
</tr>
<tr>
<td>APP-NAME</td>
<td>app-name</td>
</tr>
<tr>
<td>PROCID</td>
<td>procid</td>
</tr>
<tr>
<td>MSG-ID</td>
<td>msg-id</td>
</tr>
<tr>
<td>MSG</td>
<td>msg</td>
</tr>
</tbody>
</table>

> HTTP allows for multiple instances of a parameter to be requested with
> different values. Multiple values of the same parameter name shall be
> treated as an OR relationship for string matches. The Audit Consumer
> may combine different search parameters. The matching of different
> search parameters is combined with an AND relationship. Some examples
> of how this works are:

- To search for “hostname=Frodo” and “hostname=Bilbo” will return the
  combination of all event reports from either host Frodo or Bilbo
  during the time interval:

> <http://example.com/ARRservice/syslogsearch?date=ge2013-01-01&date=le2013-01->02&hostname=Frodo&hostname=Bilbo

- To search for “hostname=Frodo” and “proc-id=system” means all events
  from the host “Frodo” with proc-id of “system” during the time
  interval:

> <http://example.com/ARRservice/AuditEvent?date=ge2013-01-01&date=le2013-01->02&hostname=Frodo&proc-id=system

- To search for “hostname=Frodo”, “hostname=Bilbo”, and “proc-id=system”
  will return the combination of all event reports from either host
  Frodo or Bilbo that have the proc-id of “system” during the time
  interval:

> <http://example.com/ARRservice/syslogsearch?date=ge2013-01-01&date=le2013-01->02&hostname=Frodo&hostname=Bilbo
>
> This form of search is not a substitute for additional processing by
> the Audit Consumer. The Audit Record Repository can return a large
> quantity of syslog messages. The Audit Consumer may need to perform
> further processing to select the information needed for a report.
>
> The Audit Record Repository shall document in its IHE Integration
> Statement any additional parameters supported.
>
> 1295
>
> 1300
>
> 1305
>
> 1310
>
> 1315
>
> 1320
>
> 1325

###  Expected Actions

> The Audit Record Repository maintains a database of syslog messages.
> The Audit Record Repository shall return all the syslog messages
> stored in that database that match the query parameters, and which the
> requester is authorized to view (see [<u>ITI TF-1:
> 9.4</u>](https://profiles.ihe.net/ITI/TF/Volume1/ch-9.html#9.4) for
> further details). The Audit Record Repository retains data in
> accordance to local policies and some data may be deleted.
>
> The Audit Record Repository shall respond with a Syslog Event Response
> message described in Section 3.82.4.2.
>
> When performing matching based on the search parameters, the Audit
> Record Repository shall:

- Select all messages that have a time interval specified in the request
  URL.

- If search parameters other than those defined in Section 3.82.4.1.2.2
  are specified in the request URL, then if the parameter is not
  supported, it shall be ignored; otherwise, if this parameter is
  supported, the Audit Record Repository shall apply matching criteria
  in accordance to that.

- Select a response format following the rules of RFC7231 Section 5.3.2.
  The Audit Record Repository shall support JSON format (i.e.,
  application/json). In the absence of an Accept preference, JSON shall
  be used.

### Syslog Event Response Message

> The Audit Record Repository sends the Syslog Event Response message in
> response to a query from an Audit Consumer

### Trigger Events

> The Audit Record Repository creates this message when it receives and
> processes a Retrieve <span id="_bookmark83"
> class="anchor"></span>Syslog Event Request message.

### Message Semantics

> The Content-Length entity-header field shall be returned, unless this
> is prohibited by the rules in RFC2616 Section 4.4, or subsequent
> versions of the HTTP specification.
>
> Note: RFC2616 specifies that this field *should* be returned. This
> transaction strengthens that requirement.
>
> In case of success, the Audit Record Repository shall return the
> syslog messages that match the search parameters, encoded as an array
> of messages encoded in one of the formats specified in the Accept
> header of the request message. The Syslog Event Response message shall
> carry a HTTP response status code of 200, and its body shall contain
> an Array of syslog messages in the selected format.
>
> Each syslog message shall be encoded as described in Table
> 3.38.4.2.2-1:
>
> **Table 3.82.4.2.2-1: Syslog Message Encoding**

<table style="width:84%;">
<colgroup>
<col style="width: 28%" />
<col style="width: 28%" />
<col style="width: 26%" />
</colgroup>
<thead>
<tr>
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
<tr>
<td>PRI</td>
<td>Pri</td>
<td>&lt;<a
href="http://hl7.org/fhir/2015May/datatypes.html#string">string</a>&gt;</td>
</tr>
<tr>
<td>VERSION</td>
<td>Version</td>
<td>&lt;<a
href="http://hl7.org/fhir/2015May/datatypes.html#string">string</a>&gt;</td>
</tr>
<tr>
<td>TIMESTAMP</td>
<td>Timestamp</td>
<td>see RFC5424 (Sec. 6.2.3)</td>
</tr>
<tr>
<td>HOSTNAME</td>
<td>Hostname</td>
<td>&lt;<a
href="http://hl7.org/fhir/2015May/datatypes.html#string">string</a>&gt;</td>
</tr>
<tr>
<td>APP-NAME</td>
<td>App-name</td>
<td>&lt;<a
href="http://hl7.org/fhir/2015May/datatypes.html#string">string</a>&gt;</td>
</tr>
<tr>
<td>PROCID</td>
<td>Procid</td>
<td>&lt;<a
href="http://hl7.org/fhir/2015May/datatypes.html#string">string</a>&gt;</td>
</tr>
<tr>
<td>MSG-ID</td>
<td>Msg-id</td>
<td>&lt;<a
href="http://hl7.org/fhir/2015May/datatypes.html#string">string</a>&gt;</td>
</tr>
<tr>
<td>MSG</td>
<td>Msg</td>
<td>&lt;<a
href="http://hl7.org/fhir/2015May/datatypes.html#string">string</a>&gt;</td>
</tr>
<tr>
<td>STRUCTURED_DATA</td>
<td>Structured_data</td>
<td>&lt;<a
href="http://hl7.org/fhir/2015May/datatypes.html#string">string</a>&gt;</td>
</tr>
</tbody>
</table>

> 1330
>
> 1335
>
> 1340
>
> 1345
>
> 1350
>
> If the date parameter is missing, the Audit Record Repository may
> return HTTP response code 400 - Bad Request.
>
> If the specified parameters do not result in any matching syslog
> messages, the Audit Record Repository shall report a Response of
> Success (HTTP 200) with an empty JSON array.
>
> If the requested data size is excessive, the Audit Record Repository
> may respond with HTTP 206 Partial Content. If the response is 206
> Partial Content, then the response body may contain a subset of the
> syslog messages that match the search. This transaction does not
> define query result pagination mechanisms, so the Audit Consumer
> cannot query for remaining content in case of http 206 error received.
>
> If the “Accept” header provided in the Request is not supported by the
> Audit Record Repository, it may send a 415 “Unsupported Media Type”
> error.
>
> Note: Other HTTP response codes may be returned by the Audit Record
> Repository, indicating conditions outside of the scope of this
> transaction, for example, 401 – Authentication Failed might be
> returned if Audit Record Repository also supports the IUA Profile and
> is given an expired authorization token or is grouped with the EUA
> Profile Kerberized Server.
>
> The Audit Record Repository should complement the returned error code
> with a human readable description of the error condition.
>
> Audit Record Repository may return HTTP redirect responses (responses
> with values of 301, 302, 303, or 307) in response to a request. Audit
> Consumers must follow redirects, but if a loop <span id="_bookmark84"
> class="anchor"></span>is detected, it may report an error.

### JSON encoded array of Syslog Messages

> The Audit Record Repository shall construct a JSON array of syslog
> messages by parsing the message elements in each matching Syslog as
> defined in RFC5424 as strings identified by the element name in
> RFC5424. If an element is absent from the syslog message, the Audit
> Record Repository shall not include this element in the JSON encoding.
>
> 1355

<table style="width:67%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr>
<th rowspan="3"></th>
<th><p>[</p>
<blockquote>
<p>{</p>
</blockquote></th>
</tr>
<tr>
<th><blockquote>
<p>"Pri": "string",</p>
</blockquote></th>
</tr>
<tr>
<th><blockquote>
<p>"Version": "string",</p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr>
<td>1360</td>
<td><blockquote>
<p>"Timestamp": "2015-03-17T00:05",</p>
</blockquote></td>
</tr>
<tr>
<td></td>
<td><blockquote>
<p>"Hostname": "string",</p>
</blockquote></td>
</tr>
<tr>
<td></td>
<td><blockquote>
<p>"App-name": "string",</p>
</blockquote></td>
</tr>
<tr>
<td></td>
<td><blockquote>
<p>"Procid": "string",</p>
</blockquote></td>
</tr>
<tr>
<td></td>
<td><blockquote>
<p>"Msg-id": "string",</p>
</blockquote></td>
</tr>
<tr>
<td>1365</td>
<td><blockquote>
<p>"Msg": "string1",</p>
</blockquote></td>
</tr>
<tr>
<td></td>
<td><blockquote>
<p>"Structured_data": "string"</p>
</blockquote></td>
</tr>
<tr>
<td></td>
<td><blockquote>
<p>},</p>
</blockquote></td>
</tr>
<tr>
<td></td>
<td><blockquote>
<p>{</p>
</blockquote></td>
</tr>
<tr>
<td>1370</td>
<td><blockquote>
<p>"Pri": "string",</p>
<p>"Version": "string",</p>
</blockquote></td>
</tr>
<tr>
<td></td>
<td><blockquote>
<p>"Timestamp": "2015-03-17T00:05",</p>
</blockquote></td>
</tr>
<tr>
<td></td>
<td><blockquote>
<p>"Hostname": "string",</p>
</blockquote></td>
</tr>
<tr>
<td></td>
<td><blockquote>
<p>"App-name": "string",</p>
</blockquote></td>
</tr>
<tr>
<td></td>
<td><blockquote>
<p>"Procid": "string",</p>
</blockquote></td>
</tr>
<tr>
<td>1375</td>
<td><blockquote>
<p>"Msg-id": "string",</p>
</blockquote></td>
</tr>
<tr>
<td></td>
<td><blockquote>
<p>"Msg": "string2"</p>
</blockquote></td>
</tr>
<tr>
<td></td>
<td><blockquote>
<p>},</p>
</blockquote></td>
</tr>
<tr>
<td></td>
<td><blockquote>
<p>{</p>
</blockquote></td>
</tr>
<tr>
<td></td>
<td><blockquote>
<p>"Pri": "string",</p>
</blockquote></td>
</tr>
<tr>
<td>1380</td>
<td><blockquote>
<p>"version": "string",</p>
</blockquote></td>
</tr>
<tr>
<td></td>
<td><blockquote>
<p>"Timestamp": "2015-03-17T00:05",</p>
</blockquote></td>
</tr>
<tr>
<td></td>
<td><blockquote>
<p>"Hostname": "string",</p>
</blockquote></td>
</tr>
<tr>
<td></td>
<td><blockquote>
<p>"App-name": "string",</p>
</blockquote></td>
</tr>
<tr>
<td>1385</td>
<td><blockquote>
<p>"Procid": "string",</p>
<p>"Msg-id": "string",</p>
</blockquote></td>
</tr>
<tr>
<td></td>
<td><blockquote>
<p>"Msg": "string3"</p>
</blockquote></td>
</tr>
<tr>
<td></td>
<td><blockquote>
<p>}</p>
</blockquote>
<p>]</p></td>
</tr>
</tbody>
</table>

> **Figure 3.82.4.2.2.1-1: Example JSON encoded array of syslog
> messages**
>
> 1390
>
> 1395

###  Expected Actions

> The Audit Consumer shall process the response according to the
> capabilities of its application. The processing is not constrained by
> IHE.
>
> The Audit Record Repository shall create and store locally an audit
> event structured in accordance to requirements defined in DICOM PS3.15
> Section A.5.3.2 “Audit Log Used”.

### Security Considerations

> <span id="_bookmark87" class="anchor"></span>See the general Security
> Considerations in [<u>ITI TF-1:
> 9.5</u>.](https://profiles.ihe.net/ITI/TF/Volume1/ch-9.html#9.5)

### Security Audit Considerations

> This transaction may involve the disclosure of sensitive information.
> Logging these retrieval transactions as a query event is appropriate.
> However, ATNA Profile does not require the Audit
>
> 1400
>
> Record Repository to be able to send audit records using the Record
> Audit Event \[ITI-20\] transaction. The Audit Record Repository shall
> create and store locally an audit event as follows:

<table style="width:100%;">
<colgroup>
<col style="width: 15%" />
<col style="width: 29%" />
<col style="width: 7%" />
<col style="width: 47%" />
</colgroup>
<thead>
<tr>
<th style="text-align: center;"></th>
<th><blockquote>
<p><strong>Field Name</strong></p>
</blockquote></th>
<th style="text-align: center;"><strong>Opt</strong></th>
<th><blockquote>
<p><strong>Value Constraints</strong></p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="5"
style="text-align: center;"><p><strong>Event</strong></p>
<blockquote>
<p>AuditMessage/ EventIdentification</p>
</blockquote></td>
<td><blockquote>
<p>EventID</p>
</blockquote></td>
<td style="text-align: center;">M</td>
<td>EV <a
href="http://dicom.nema.org/medical/dicom/current/output/chtml/part16/chapter_D.html#DCM_110101">(110101,
DCM, "Audit Log Used")</a></td>
</tr>
<tr>
<td><blockquote>
<p>EventActionCode</p>
</blockquote></td>
<td style="text-align: center;">M</td>
<td>“R” (Read)</td>
</tr>
<tr>
<td><blockquote>
<p><em>EventDateTime</em></p>
</blockquote></td>
<td style="text-align: center;"><em>U</em></td>
<td><em>not specialized</em></td>
</tr>
<tr>
<td><blockquote>
<p><em>EventOutcomeIndicator</em></p>
</blockquote></td>
<td style="text-align: center;"><em>U</em></td>
<td><em>not specialized</em></td>
</tr>
<tr>
<td><blockquote>
<p>EventTypeCode</p>
</blockquote></td>
<td style="text-align: center;">M</td>
<td>EV(“ITI-82”, “IHE Transactions”, “Retrieve Syslog Event”)</td>
</tr>
<tr>
<td colspan="4" style="text-align: center;">Source (Audit Consumer)
(1)</td>
</tr>
<tr>
<td colspan="4" style="text-align: center;">Human Requestor (0..1)</td>
</tr>
<tr>
<td colspan="4" style="text-align: center;">Destination (Audit Record
Repository) (1)</td>
</tr>
<tr>
<td colspan="4" style="text-align: center;">Audit Source (Audit Record
Repository) (1)</td>
</tr>
<tr>
<td colspan="4" style="text-align: center;">Syslog message (0,..n)</td>
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
<tr>
<th><blockquote>
<p><strong>Source</strong></p>
</blockquote></th>
<th><em>UserID</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="6"><blockquote>
<p>AuditMessage/ ActiveParticipant</p>
</blockquote></td>
<td>AlternativeUserID</td>
<td style="text-align: center;">M</td>
<td><blockquote>
<p>The process ID as used within the local operating system in the local
system logs.</p>
</blockquote></td>
</tr>
<tr>
<td><em>UserName</em></td>
<td style="text-align: center;"><em>U</em></td>
<td><blockquote>
<p><em>not specialized</em></p>
</blockquote></td>
</tr>
<tr>
<td><em>UserIsRequestor</em></td>
<td style="text-align: center;"><em>U</em></td>
<td><blockquote>
<p><em>not specialized</em></p>
</blockquote></td>
</tr>
<tr>
<td>RoleIDCode</td>
<td style="text-align: center;">M</td>
<td><blockquote>
<p>EV(110153, DCM, “Source Role ID”)</p>
</blockquote></td>
</tr>
<tr>
<td>NetworkAccessPointTypeCode</td>
<td style="text-align: center;">M</td>
<td><blockquote>
<p>“1” for machine (DNS) name, “2” for IP address</p>
</blockquote></td>
</tr>
<tr>
<td>NetworkAccessPointID</td>
<td style="text-align: center;">M</td>
<td><blockquote>
<p>The machine name or IP address.</p>
</blockquote></td>
</tr>
</tbody>
</table>

> 1405

<table>
<colgroup>
<col style="width: 16%" />
<col style="width: 29%" />
<col style="width: 6%" />
<col style="width: 47%" />
</colgroup>
<thead>
<tr>
<th rowspan="7" style="text-align: center;"><blockquote>
<p><strong>Human Requestor (if known)</strong></p>
<p>AuditMessage/ ActiveParticipant</p>
</blockquote></th>
<th>UserID</th>
<th style="text-align: center;">M</th>
<th><blockquote>
<p>Identity of the human that initiated the transaction.</p>
</blockquote></th>
</tr>
<tr>
<th><em>AlternativeUserID</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr>
<th><em>UserName</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr>
<th><em>UserIsRequestor</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr>
<th>RoleIDCode</th>
<th style="text-align: center;">M</th>
<th><blockquote>
<p>Access Control role(s) the user holds that allows this
transaction.</p>
</blockquote></th>
</tr>
<tr>
<th><em>NetworkAccessPointTypeCode</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr>
<th><em>NetworkAccessPointID</em></th>
<th style="text-align: center;"><em>U</em></th>
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
<tr>
<th><blockquote>
<p><strong>Destination</strong></p>
</blockquote></th>
<th>UserID</th>
<th style="text-align: center;">M</th>
<th><blockquote>
<p>SOAP endpoint URI.</p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="2"><blockquote>
<p>AuditMessage/ ActiveParticipant</p>
</blockquote></td>
<td><em>AlternativeUserID</em></td>
<td style="text-align: center;"><em>U</em></td>
<td><blockquote>
<p><em>not specialized</em></p>
</blockquote></td>
</tr>
<tr>
<td><em>UserName</em></td>
<td style="text-align: center;"><em>U</em></td>
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
<tr>
<th rowspan="4"></th>
<th><em>UserIsRequestor</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr>
<th>RoleIDCode</th>
<th style="text-align: center;">M</th>
<th><blockquote>
<p>EV(110152, DCM, “Destination Role ID”)</p>
</blockquote></th>
</tr>
<tr>
<th>NetworkAccessPointTypeCode</th>
<th style="text-align: center;">M</th>
<th><blockquote>
<p>“1” for machine (DNS) name, “2” for IP address</p>
</blockquote></th>
</tr>
<tr>
<th>NetworkAccessPointID</th>
<th style="text-align: center;">M</th>
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
<tr>
<th rowspan="3" style="text-align: center;"><blockquote>
<p><strong>Audit Source</strong></p>
</blockquote>
<p>AuditMessage/AuditSou rceIdentification</p></th>
<th><em>AuditSourceID</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><em>not specialized</em></th>
</tr>
<tr>
<th><em>AuditEnterpriseSiteID</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><em>not specialized</em></th>
</tr>
<tr>
<th><em>AuditSourceTypeCode</em></th>
<th style="text-align: center;"><em>U</em></th>
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
<tr>
<th rowspan="9" style="text-align: center;"><blockquote>
<p><strong>Syslog message</strong></p>
<p>AuditMessage/ ParticipantObjectIdentif ication</p>
</blockquote></th>
<th>ParticipantObjectTypeCode</th>
<th style="text-align: center;">M</th>
<th><blockquote>
<p>“2” (System object)</p>
</blockquote></th>
</tr>
<tr>
<th>ParticipantObjectTypeCodeRole</th>
<th style="text-align: center;">M</th>
<th><blockquote>
<p>“13” (Security Resource)</p>
</blockquote></th>
</tr>
<tr>
<th><em>ParticipantObjectDataLifeCycle</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr>
<th>ParticipantObjectIDTypeCode</th>
<th style="text-align: center;">M</th>
<th><blockquote>
<p>EV(“12”, “RFC-3881”, "URI")</p>
</blockquote></th>
</tr>
<tr>
<th><em>ParticipantObjectSensitivity</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr>
<th>ParticipantObjectID</th>
<th style="text-align: center;">M</th>
<th><blockquote>
<p>The URI of the Audit log</p>
</blockquote></th>
</tr>
<tr>
<th>ParticipantObjectName</th>
<th style="text-align: center;">U</th>
<th><blockquote>
<p>“Security Audit Log”</p>
</blockquote></th>
</tr>
<tr>
<th><em>ParticipantObjectQuery</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
<tr>
<th><em>ParticipantObjectDetail</em></th>
<th style="text-align: center;"><em>U</em></th>
<th><blockquote>
<p><em>not specialized</em></p>
</blockquote></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

> *Editor: Update the “Appendix Z on HL7 FHIR” TI supplement, Section
> Z.8:*
>
> 1415
>
> 1420
>
> 1425

##  Z.8 Mobile Security Considerations

> There are many security and privacy concerns with mobile devices,
> including lack of physical control. Many common information
> technologies use of HTTP, including REST, access far less sensitive
> information than health information. These factors present an
> especially difficult challenge for the security model. Application
> developers should perform a Risk Assessment during design of their
> applications, and organizations responsible for the operational
> environment should perform Risk Assessments on the design and
> deployment of the operational environment. See FHIR Security and
> Privacy Module
> [<u>http://hl7.org/fhir/R4/secpriv-module.html</u>](http://hl7.org/fhir/R4/secpriv-module.html).
>
> Actors should not communicate any patient information unless proper
> authentication, authorization, and communications security have been
> performed.
>
> There are many reasonable methods of securing interoperability
> transactions. These security models can be layered in without
> modifying the characteristics of the transaction. The use of TLS is
> encouraged, specifically the use of the ATNA Profile. User
> authentication on mobile devices is encouraged using Internet User
> Authorization (IUA) Profile. The IUA Profile is a profile of the OAuth
> protocol. IUA enables external Authorization providers, which can
> leverage pluggable authentication providers, such as OpenID Connect.
> The network communication security and user authentication are layered
> in at the HTTP transport layer and do not modify the interoperability
> characteristics defined in the transaction.
>
> 1430
>
> 1435
>
> 1440
>
> 1445

###  ~~Security audit logging (e.g., ATNA) is recommended. Support for ATNA-based audit~~ logging on the mobile health device may be beyond the ability of the client-constrained environment. For example, the client actor may only support HTTP interactions using ~~JSON encoding, while the Record Audit Event \[ITI-20\] transaction requires the SYSLOG~~ ~~protocol and XML encoding. For this reason, the use of ATNA Audit Logging is not~~ ~~mandated. This means that the organization responsible for the operational environment~~ ~~must choose how to mitigate the risk of relying only on the service side audit logging.~~

> **<u>Security audit logging (e.g., ATNA) is recommended. Support for
> ATNA-based audit</u> logging on the mobile health device can be done
> using the Record Audit Event \[ITI-20\] <u>transaction that supports
> HTTP interactions for both JSON and XML encoding.</u>**
>
> Many transactions using HTTP REST will include query parameters that
> would be identifiers, quasi-identifiers, or sensitive health topics.
> For example, it is common for patient identifier to be a query
> parameter. With this URL pattern, the query parameters are typically
> visible in the server audit log or browser history. The risk from this
> visibility should be mitigated in system or operational design, by
> protecting the logs as sensitive data, or by designing other measures
> into the system to prevent inappropriate exposure.
