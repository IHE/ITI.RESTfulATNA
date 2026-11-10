This supplement extends the functionalities of the ATNA Profile by introducing RESTful operations that could be used to submit and retrieve audit records. This allows light weight applications to easily manage the creation and the access audit information. This supplement is based on FHIR protocol and uses FHIR AuditEvent Resources in order to exchange audit records content. This supplement also defines a query transaction that enables access to raw syslog messages.

<div markdown="1" class="stu-note">

| [Significant Changes, Open and Closed Issues](issues.html) |
{: .grid}

</div>

### Organization of This Guide

This guide is organized into the following sections:

1. Volume 1: Actors, Transactions and Use Cases
   1. [Introduction](volume-1.html)
   2. [Actors, Transactions, and Content](volume-1.html#actors-and-transactions)
   3. [Actor Options](volume-1.html#actor-options)
   4. [Use Cases](volume-1.html#use-cases)
   5. [Security Considerations](volume-1.html#security-considerations)
2. Volume 2: Transaction Detail
   1. [Record Audit Event [ITI-20]](ITI-20.html)
   2. [Retrieve ATNA Audit Event [ITI-81]](ITI-81.html)
   3. [Retrieve Syslog Event [ITI-82]](ITI-82.html)
3. Other
   1. [Changes to Other IHE Specifications](other.html)
   2. [Download and Analysis](download.html)
   3. [Test Plan](testplan.html)

See also the [Table of Contents](toc.html) and the index of [Artifacts](artifacts.html) defined as part of this implementation guide.

### Conformance Expectations

IHE uses the normative words: "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" according to [standards conventions](https://profiles.ihe.net/GeneralIntro/ch-E.html).

#### Must Support

The use of ```mustSupport``` in StructureDefinition profiles equivalent to the IHE use of **R2** as defined in [Appendix Z](https://profiles.ihe.net/ITI/TF/Volume2/ch-Z.html#z.10-profiling-conventions-for-constraints-on-fhir).

mustSupport of true - only has a meaning on items that are minimal cardinality of zero (0), and applies only to the source actor populating the data. The source actor shall populate the elements marked with MustSupport, if the concept is supported by the actor, a value exists, and security and consent rules permit.
The consuming actors should handle these elements being populated or being absent/empty.
Note that sometimes mustSupport will appear on elements with a minimal cardinality greater than zero (0), this is due to inheritance from a less constrained profile.
