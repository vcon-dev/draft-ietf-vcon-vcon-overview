---
title: "The vCon - Conversation Data Container - Overview"
abbrev: "vCon Overview"
category: info

docname: draft-ietf-vcon-overview-latest

submissiontype: IETF  # also: "independent", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
area: "Applications and Real-Time"
workgroup: "Virtualized Conversations"
keyword:
 - conversation
 - vcon
 - CDR
 - call detail record
 - call meta data
 - call recording
 - email thread
 - text conversation
 - video recording
 - video conference
 - conference recording
venue:
  group: "Virtualized Conversations"
  type: "Working Group"
  mail: "vcon@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/vcon/"
  github: "ietf-wg-vcon/draft-ietf-vcon-overview"
  latest: "https://ietf-wg-vcon.github.io/draft-ietf-vcon-overview/draft-ietf-vcon-overview.html"

author:
 -
    fullname: Thomas McCarthy-Howe
    organization: Strolid
    email: thomas.howe@strolid.com

normative:

  RFC3339:


informative:

# TODO:  the following were normative in the container I-D.  Most can probably be deleted.

  GEOPRIV: RFC4119

  GZIP: RFC1952

  HTTPS: RFC9110

  IANA-COSE-ALG:
    target: <https://www.iana.org/assignments/cose/cose.xhtml>
    title: "COSE Algorithms"

  JSON: RFC8259

  JWS: RFC7515

  JWE: RFC7516

  JWK: RFC7517

  MAILTO: RFC6068

  MEDIATYPE: RFC6838

  MIME: RFC2045

  PASSporT: RFC8225

  PIDF-LO: RFC5491

  SMTP: RFC5321

  TEL: RFC3966

  UUID: I-D.draft-peabody-dispatch-new-uuid-format

#TODO:  end formerly normative references.  Many of the following informationaly references can probably also be deleted from this overview I-D

  CBOR: RFC8949

  CDDL: RFC8610

  ISOBMFF:
    target: https://www.iso.org/standard/83102.html
    title: "Information technology -- Coding of audio-visual objects -- Part 12: ISO base media file format"
    refcontent: ISO/IEC 14496-12:2022
    date: 2022-01

  JMAP: RFC8620

  JWT: RFC7519

  SHA-512: RFC6234

  SIP-XFER: RFC5589

  STIR-PASS: I-D.draft-ietf-stir-passport-rcd

  vCard: RFC7095

  vCon-white-paper:
    target: https://github.com/vcon-dev/vcon/blob/main/docs/vCons_%20an%20Open%20Standard%20for%20Conversation%20Data.pdf
    title: "vCon: an Open Standard for Conversation Data"
    author:
      -
        ins: T. Howe
        name: Thomas Howe
        org: STROLID Inc.
      -
        ins: D. Petrie
        name: Daniel Petrie
        org: SIPez LLC
      -
        ins: M. Lieberman
        name: Mitch Lieberman
        org: Conversational X
      -
        ins: A. Quayle
        name: Alan Quayle
        org: TADHack and TADSummit

  CDR:
    target: https://www.itu.int/rec/T-REC-Q.825
    title: "Recommendation Q.825: Specification of TMN applications at the Q3 interface: Call detail recording"
    date: 1998
    author:
      org: ITU

  PY-VCON:
    target: https://github.com/py-vcon/py-vcon
    title: "Python open source vCon command line interface, library and workflow server"
---

--- abstract

A vCon is the container for data and information relating to a real-time, human conversation.
It is analogous to a {{vCard}} which enables the definition, interchange and storage of an individual's various points of contact.
The data contained in a vCon may be derived from any multimedia session, traditional phone call, video conference, SMS or MMS message exchange, webchat or email thread.
The data in the container relating to the conversation may include Call Detail Records (CDR), call meta data, participant identity information (e.g. STIR PASSporT), the actual conversational data exchanged (e.g. audio, video, text), realtime or post conversational analysis and attachments of files exchanged during the conversation.
A standardized conversation container enables many applications, establishes a common method of storage and interchange, and supports identity, privacy and security efforts (see {{vCon-white-paper}}).

--- middle

# Introduction

The generation of conversational data, contained in transcripts and multi-media files, is common in business, especially in customer facing organizations.
However, the storage, analysis and sharing of the data they contain is not currently a standard, hampering efforts for both system interoperation and responsible data handling.
Standardizing a container for conversation data (vCon) has numerous advantages, and enables the management of the conversation's content.

Often the system providing the communications service, the consumer and/or owner of the communications data and the communications analysis services are distinct systems and in many case separate business entities.
vCons provide a standard means of exchanging communications data between these systems and services.
The use of vCons can ease service integration by using a common container and format for enterprise communications, becoming the standardized input to communication analysis tools and machine learning and categorization.

* For organizations in dialog with customers or citizens, a vCon can be the container of where  conversations are stored and personal data protections are expressed, managed and governed.
* For conversations of record, the vCon can be a legal instrument, providing a testable expression of conversational fact, while enabling conversational trust and transparency.
* For machine learning efforts, vCons can track what information was used in the training of models. As the result of a customer right to know request, an accurate answer to how their data was processed can be derived and communicated, and as the result of customer correction or deletion request, the responsible organization can properly and ethically respond as required by governing law.

## What's in a vCon?

A vCon contains four major categories of data (parties , dialog , analysis and attachments), with descriptive identifiers and metadata (unique id, timestamps, subject and summaries, references to related or earlier versions of the vCon), inside a JSON container that can be signed and encrypted.
The parties portion allows for an expanded set of data from a typical call detail record ([CDR]), with identifications of the participants or parties to the conversation.
The dialog portion contains a set of multimedia and media type elements, each representing the actual, physical conversation in original media form: text, audio, video and imagery.
The analysis portion contains data derived from the party and dialog portions, intended to carry items like transcripts, translations, summaries, text to speech, sentiment analysis and other semantic tagging.
Finally, the attachment portion contains any other documents, such as slide deck or sales lead information, expressions of consent or authenticity, which provides context and support for the conversation itself.
In addition to these four major categories, the vCon itself has metadata, such as unique identifiers, timestamps and references to other vCons through redaction or grouping.  The vCon may also contain integrity checking information such as the issuer of the vCon and tamper-proof features such as signatures.
vCons may also include registered extensions, and some extensions can be marked critical; see the core specification for details.

## Data Responsibility: Privacy vs Utility

Since vCons are designed to carry conversational data between systems, they must provide the ability to balance the utility and sensitivity of the information they contain.
The transmission of information outside of a security boundary does not release the controller of the data from the responsibility of handing personal data.
vCons enable the best practices of personal data management through approaches such as data minimization, consent validation and integrity protection.

The parties section carries significant privacy implications and responsibilities; the very definition of the sensitive biometric data addressed by the GDPR.
Each party identified in a vCon represents an individual or entity whose personal information is being captured and potentially shared.
The vCon creator and any subsequent processors of the vCon have a responsibility to ensure that the collection, storage, and sharing of party information complies with applicable privacy laws and regulations (such as GDPR, CCPA, or other regional privacy frameworks).
This includes obtaining appropriate consent for data collection, implementing data minimization practices, and providing mechanisms for data subjects to exercise their rights regarding their personal information.

At the same time, the conversations defined by the vCon carry the most authentic and important data in many scenarios from healthcare to commerce; a powerful addition to any data set.
To enable adoption, the JSON format implemented by the vCon is the lingua franca of modern software; a frictionless integration to applications that require the human conversation.
It is expected that JavaScript handling of vCons in the front end and RESTful interfaces and back end platforms will be used for operations and manipulation of vCons.
Many media analysis services which will be used with vCons, such as transcription, already use JSON based interfaces.
For these reasons, JSON has been chosen for the initial format binding of vCons and the scope of this document.
Other bindings (e.g. [CBOR] or [CDDL]) may be consider for vCon in the future in other documents.

### Core Privacy Principles

Modern privacy regulations establish fundamental principles that govern the collection, processing, and management of personal data. The vCon framework is designed to support these principles throughout the conversation lifecycle.

**Data Subject Rights** are central to privacy protection. Individuals whose conversations are captured in vCons have rights including the right to access their data, the right to rectification of inaccurate information, the right to erasure (also known as the "right to be forgotten"), and the right to data portability. The vCon structure enables these rights by providing clear identification of parties, maintaining relationships between vCon versions through redaction and appending mechanisms, and supporting the creation of redacted vCons that remove personal information while preserving conversation context.

**Purpose Limitation** requires that personal data be collected for specified, explicit, and legitimate purposes and not further processed in a manner incompatible with those purposes. vCons support purpose limitation through structured mechanisms for documenting the intended use of conversation data. Analysis and attachment sections can carry explicit purpose declarations, and extensions enable the expression of consent or other lawful bases tied to specific processing purposes.

**Data Minimization** is the practice of limiting the collection and processing of personal data to what is necessary for the stated purpose. vCons facilitate data minimization in several ways: parties information can be limited to only what is necessary for the use case; dialog content can reference external storage rather than embedding full media inline; redacted vCons enable sharing of limited information while maintaining verifiable links to complete versions; and analysis sections can be selectively included based on actual processing needs.

**Storage Limitation** requires that personal data be kept in a form that permits identification of data subjects for no longer than necessary. While vCons themselves do not enforce retention policies, their structured format and versioning capabilities support storage limitation practices. Organizations can track vCon lifecycles, implement automated expiration based on metadata timestamps, create time-limited redacted versions for specific purposes, and maintain audit trails of when vCons were created, modified, and should be deleted.

### Data Roles and Responsibilities

Privacy regulations distinguish between different roles in data processing, each carrying distinct responsibilities and legal obligations. Understanding these roles is essential for proper vCon lifecycle management.

The **Data Controller** is the entity that determines the purposes and means of processing personal data. In the vCon context, the controller decides what conversations to record, how long to retain them, what analysis to perform, and with whom to share the data. The controller bears primary responsibility under privacy laws and must ensure that all processing has a lawful basis, that data subjects are informed, and that appropriate technical and organizational measures are in place.

The **Data Processor** acts on behalf of the controller, processing personal data according to the controller's instructions. In vCon workflows, processors might include transcription services, sentiment analysis providers, or storage platforms. Processors have a duty to process data only as instructed, implement appropriate security measures, and assist controllers in fulfilling data subject rights requests. The relationship between controllers and processors is typically governed by data processing agreements that specify the scope and terms of processing.

**Accountability** is a fundamental principle requiring organizations to demonstrate compliance with privacy obligations. For vCons, accountability means maintaining records of processing activities, documenting lawful bases for data collection and use, implementing privacy by design principles in vCon handling systems, and being able to prove appropriate handling in response to regulatory inquiries. The structured nature of vCons, combined with cryptographic signing capabilities, supports accountability by creating verifiable records of what data was collected, when it was processed, and how it was shared.

These roles matter throughout the vCon lifecycle because as vCons move between organizations, responsibilities may shift, and clear documentation of who controls the data at each stage is essential for proper privacy governance.

### Communications Privacy

Conversations involve unique privacy considerations beyond general data protection. The act of recording, storing, and analyzing human communications raises specific legal and ethical questions that vary by jurisdiction and context.

**Consent models** for conversation recording differ significantly across legal frameworks. Some jurisdictions follow a one-party consent model, where only one participant in a conversation needs to consent to recording. Others require all-party consent, where every participant must agree before recording can occur. Still others permit recording only with explicit, informed consent documented before the conversation begins. vCons are designed to be neutral regarding consent models; they can carry consent information through attachments or extensions, document when and how consent was obtained, and support different consent mechanisms appropriate to the applicable legal framework. The choice of consent model and its implementation remains a deployment decision based on jurisdictional requirements.

**Reasonable expectation of privacy** is a legal concept that influences when conversation recording is permissible. A person generally has a reasonable expectation of privacy in conversations held in private spaces, in intimate discussions, or when the circumstances suggest confidentiality. This expectation diminishes in public spaces, business contexts with clear policies, or when participants are aware of recording. vCons support privacy expectations through clear metadata about conversation context, the ability to document notification and consent, and mechanisms for redacting sensitive portions while preserving non-sensitive content.

**Notice requirements** mandate informing individuals that their conversations are being recorded or monitored. Notice may be provided through explicit announcements, signage, terms of service, or automated messages at the beginning of calls. Adequate notice typically explains what is being recorded, why the recording is occurring, how the data will be used, and who will have access to it. The structured nature of vCons enables organizations to attach notice text, document when notice was provided, reference applicable policies, and maintain records demonstrating compliance with notice requirements.

These communications privacy principles intersect with the broader data protection framework to create specific obligations for conversation data. Organizations using vCons must consider both general privacy principles and communications-specific requirements when designing their conversation management systems.

For most application architectures, JSON objects are created by applications, for applications.
However, most of the initial set of use cases for differ from this established pattern, and are expected to be in the interchange between front end and back end application and lower layers of the network stack, critical for enablement of analysis of conversations.
Thus, the contents of the vCon, if not the vCon itself, are generated by various and diverse network and communications elements like SIP user agents and SMTP servers, and then delivered across networks, and sometimes across security boundaries.
This diversity of conversational data creates difficulty in creating unified views of customer conversations, especially as they traverse conversational modes.
By providing a common mechanism to describe conversations, appropriate to the various network elements that create them, enables new scenarios and usage kinds.

## Use Cases and Requirements

### Contact Center Use Case

Contact centers typically handle customer interactions across multiple communication channels including voice telephony, web-based chat systems, electronic mail, Short Message Service (SMS), and video conferencing platforms.  Each interaction channel generates conversational data that is often stored in disparate systems using incompatible formats, creating operational challenges for organizations seeking to maintain comprehensive customer interaction records, perform cross-channel analytics, or implement consistent privacy management practices.

A vCon-based implementation addresses these challenges by establishing a standardized container format for each interaction while maintaining referential relationships between related conversations.  When a customer interaction spans multiple channels (e.g., initial web chat escalated to video conference with email follow-up), each communication system generates a vCon containing the conversation parties, dialog content, automated analysis results, and relevant attachments.  These vCons are linked through common case identifiers and sequential references, enabling downstream systems to reconstruct complete customer interaction timelines while preserving the integrity and context of each individual conversation component.

The implementation of vCons in contact center environments provides several operational benefits: unified customer journey tracking across all communication channels, enhanced analytics capabilities through standardized data formats, simplified regulatory compliance through consistent consent tracking and audit trails, efficient privacy rights management with granular data deletion and redaction capabilities, and improved quality assurance processes through comprehensive evaluation of multi-channel customer service interactions.  This standardization reduces operational complexity while ensuring compliance with applicable privacy regulations.

### Messaging Use Case

Healthcare organizations providing patient communication services across multiple messaging platforms including SMS, secure patient portals, electronic mail, and integrated telehealth systems face significant challenges in maintaining complete medical communication records while ensuring compliance with healthcare privacy regulations such as the Health Insurance Portability and Accountability Act (HIPAA).  Patient conversations frequently span multiple communication channels over extended periods, resulting in fragmented medical records that impede clinical decision-making and complicate regulatory compliance efforts.

A vCon implementation in healthcare messaging environments employs privacy-preserving design principles including explicit consent management, data minimization capabilities, healthcare-grade encryption standards, and role-based access controls.  Each communication channel creates a vCon instance containing conversation participants, message content, automated analysis results, and relevant medical attachments, while maintaining integration pathways with Electronic Health Record (EHR) systems.  This architecture enables authorized healthcare providers to access complete patient communication histories for care coordination purposes while implementing granular privacy controls to protect sensitive health information in accordance with applicable regulations.

The deployment of vCons in healthcare messaging systems delivers measurable improvements including comprehensive patient communication records integrated with clinical data systems, enhanced privacy protection through granular control mechanisms for sensitive health information, improved care coordination between multiple healthcare providers, built-in regulatory compliance capabilities with automated audit trails and consent management, and enhanced clinical decision support through access to complete patient communication context.  This standardization enables healthcare organizations to improve patient care delivery while maintaining strict privacy protection and regulatory compliance requirements.

### ECRIT (Emergency Context Resolution with Internet Technologies) Use Case

Emergency services organizations require rapid access to comprehensive situational information during crisis response operations.  Traditional emergency communication systems create information silos where critical multimedia content, geographic location data, and inter-agency coordination communications are distributed across multiple systems and jurisdictional boundaries.  This fragmentation delays access to vital operational information, complicates multi-agency coordination efforts, and produces incomplete documentation for subsequent legal proceedings and incident investigations.

A vCon implementation for emergency services enables real-time creation and maintenance of linked conversation containers that capture initial emergency calls, multimedia updates from incident witnesses, location tracking data, multi-agency coordination communications, and post-incident investigation records.  Each vCon contains conversation participants (emergency callers, dispatchers, response personnel), dialog content (voice recordings, text messages, radio communications), automated analysis results (emergency classification, resource requirements, incident reconstruction), and relevant attachments (photographs, videos, location coordinates, official reports).  Critical operational features include real-time vCon creation and updates, priority processing mechanisms, cryptographic integrity protection, and secure multi-jurisdictional information sharing capabilities.

The implementation of vCons in emergency services environments provides operational improvements including complete situational awareness for emergency response personnel, reduced response times through expedited access to critical information, enhanced inter-agency coordination through standardized information sharing protocols, regulatory compliance through complete tamper-evident record keeping, and improved public safety outcomes through enhanced information management capabilities.  Integration with existing emergency services infrastructure including Computer-Aided Dispatch (CAD) systems, Geographic Information Systems (GIS), and Next Generation 911 (NG911) platforms ensures that vCon implementation enhances rather than replaces current emergency response capabilities.

## Requirements

An outline of the vCon requirements derived from the explored use case follows:

* Standardize container for conversational data exchange
* Consolidation of data and information for a conversation
* Multiple modes of communication, changing over time
* Snapshots of conversation during or once completed along with analysis
* Ease of integration of services and analysis
* Better organize conversational data so that it can be handled in a consistent, privacy safer means
* Immutable once signed or encrypted
* Hiding of PII or entire conversation
* Amendable with additional information and data elements

Define a standard for exchange of conversational data in a sea of modes, platforms and service offerings for conversations.

Example conversational modes and protocols:

* SMS
* MMS
* JABBER
* SIMPLE
* Proprietary web chat
* SMTP
* PSTN
* SIP
* WEBRTC
* Proprietary video conferencing

The following  are considered not in scope or non-requirements:

* Real-time streaming or updating of conversational data
* Transport mechanisms
* Storage or databases specifications
* Media-specific redaction algorithms for text, audio or video
* Advanced validation of redactions or appended data beyond signatures (e.g. Merkle tree like redactions)
* Standardization of analysis data formats or file media types

# Conventions and Definitions

{::boilerplate bcp14-tagged}

## Terminology

* analysis - analysis, transformations, summary, sentiment, or translation typically of the dialog data
* conversation - an exchange of communication using text, audio or video medium between at least one human and one or more bots or humans
* consent - explicit permission granted by a party for the collection, processing, or sharing of their conversation data
* data minimization - the practice of limiting the collection and processing of personal data to what is necessary for the stated purpose
* de-identification - removal of all information that could identify a party in a conversation. This includes PII as well as audio and video recordings. Voice recordings might be re-vocalized with a different speaker.
* dialog - the captured conversation in its original form (e.g. text, audio or video)
* encrypted form - encrypted JWE document with the JWS signed vCon form contained in the ciphertext
* file - a data block either included or referenced in a vCon
* object - JSON object containing key and value pairs
* parameter - JSON key and value pair
* party - an observer or participant to the conversation, either passive or active
* payload - the contents or bytes that make up a file
* PII - Personal Identifiable Information
* PII masked - may include voice recordings, but PII is removed from transcripts and recordings (audio and video)
* redaction - the process of removing or obscuring specific content from a vCon while maintaining the overall structure and integrity
* signed form - JWS signed document with the unsigned vCon form contained in the payload
* vCon - container for conversational information
* vCon instance - a vCon populated with data for a specific conversation
* vCon instance version - a single version of an instance of a conversation, which may be modified to redact or append additional information forming a subsequent vCon instance version
* vCon extension - a registered schema addition; some extensions may be marked critical

## Inline vs Externally Referenced Files

Due to the size and complexity of some portions of a vCon, both inline and externally referenced dialog, analysis, attachments and other vCon reference assets are supported.
For instance, vCons may reference a video conference media recording as an external URL with an accompanying content hash of the contents to detect tampering.
Alternatively, vCons may directly contain the media of the entire dialog internally, keeping the conversation in one place, and optionally encrypted.
External content should be signed and transported over HTTPS; vCons sent over non-secure channels should be encrypted.

# vCon JSON Object

## A Conversational Definition

vCons define conversations, and are created by systems during and after the conversation itself.
vCons provide ways to express and define the contents, participants and context of a particular conversation.
Unlike some measureable physical phenomena, like mass and volume, conversations are heterogeneous, relatively complex and contain relevant information outside of the physical phenomena, such as consent and provenance.
Some communication modes, like SMS texting, lack natural session boundaries and require explicit definition.
Thus, the definition of a conversation requires more than a simple scalar value, or a series of samples of a time-based waveform.
The definition of a conversation enables tools and systems to precisely identify, responsibly manage, efficiently process and accurately govern their use.

vCons also enables the definer of the conversation to express the scope of the conversations.
A vCon may contain any combination of content appropriate to the use case:

* A vCon may be a single audio recording, or a complete conversational journey from a text message, to a resulting conversation and a followup email.
* A vCon may represent a conversation between two people, a conversation between a person and a machine, or all of the conversations between customers and a contact center team.
* A vCon may be sent in response to a Right To Know request to a single customer, or to a governance body during an audit

None of the major parts of the vCon (parties, dialog, attachments and analysis) are required to be present, to maximize the conversations that can be expressed.
For instance, a recording without a parties definition is a valid expression of a conversation without defining the people involved, either because it is unknown, to be discovered through the analysis of the recording, or to be hidden for data minimization reasons.
vCons may have two or more parties involved, but since a fundamental role of the vCon is to define and protect the data it contains, at least one should be, in the words of the GDPR, a "natural person." Future protocol versions or extensions may focus on more inter-machine conversations, as the fundamental parts of conversation are not dissimilar between the two use cases.

## Parties

The parties section in a vCon serves as the container for all participant identity information involved in the conversation.
Structurally, it is an array of party objects, each of which can include various attributes such as telephone numbers, email addresses, names, and even structured contact information (like civic addresses and geographic coordinates).
The purpose of this section is to provide clear attribution of every interaction by documenting who participated in the conversation.
This not only supports accurate record-keeping but also enables accountability, context, and subsequent analysis of the conversation data.

For example, as defined by the vCon standard, each party object may contain fields such as telephone numbers, email addresses, participant names, and more detailed address and identification data.
This detailed structure ensures that each participant can be uniquely identified and that their roles (such as agent or customer) are clearly established within the conversation record.

The identification of parties serves multiple purposes beyond simple attribution.
It enables proper consent management by clearly identifying whose data is being processed, supports data subject rights requests by providing a clear mapping of individuals to their conversation data, and facilitates compliance with privacy regulations that require organizations to track and manage personal data throughout its lifecycle.
Additionally, the structured nature of party identification allows for consistent handling of privacy-related operations such as data deletion, anonymization, or redaction requests across different systems and jurisdictions.

## Dialog

The dialog section in a vCon captures the actual conversation content that occurred between parties. This is the core of what makes a vCon valuable - it contains the real communication that took place, whether that was spoken words, text messages, or other forms of interaction. The dialog section serves as the primary record of what was said, when it was said, and who was involved in each exchange. Dialogs contain the "ground truths" of the conversation.

Each dialog entry represents a distinct communication event within the broader conversation. This could be a single text message, a phone call, a video conference session, or any other form of communication. The dialog section maintains the chronological flow and context of the conversation, preserving not just what was communicated, but the timing and sequence of exchanges that give meaning to the interaction.

The identification and tracking of dialog content serves critical privacy and compliance functions. The structured format enables precise identification of which specific conversations contain personal information, allowing for targeted data subject rights fulfillment such as selective deletion of specific dialog segments rather than entire conversation records. The timestamp and party reference metadata provide essential context for privacy impact assessments and data retention decisions. Additionally, the content hash mechanism ensures data integrity while also enabling verification that external content has not been tampered with, which is crucial for maintaining the trustworthiness of conversation records in legal or compliance contexts.

The purpose of the dialog section is two-fold:

* **Content Representation**: It accurately captures the details of any conversation exchange—be it spoken words, text messages, or other communication types.
  This ensures that the exact sequence and content are archived in a standardized format.
  The content appropriate to dialogs are any of the times and places where personal data is communicated and recorded: audio, video, email, fax, rich emails as examples.
* **Interoperability and Analysis**: The dialog's structured format supports further analysis (such as transcription or sentiment analysis) and ensures that conversations can be reliably exchanged between systems. By storing metadata like timestamps and participant references, the dialog section also enables the reconstruction of events (such as when participants join or leave a conversation) and aids in analytic processing.

In summary, the dialog section is critical for recording, storing, and later analyzing the actual conversation data within a vCon object.

## Attachments

Attachments carry the context of the conversation; storing supplemental files and data that support the conversation record.
In the vCon, attachments are designed as an array of opaque objects.
They can be documents, images or any valid mediatype that can serve the proper analysis and comprehension of the conversation by providing context.
In them, they may contain expressions of consent, references to content authenticity, authorization receipts and business tracking objects.

In parallel with each opaque object is a set of metadata that enables semantic understanding of the contents without the exposure of the underlying data.
Attachment metadata contains information such as the type of data it contains, the party or dialog it refers to, and whether or not the data is contained in the attachment itself, or is referenced by external network identifier.

## Analysis

The analysis section of a vCon contains processed insights and derived information from the original conversation data,
serving as a bridge between the raw conversation data and business intelligence applications.
The analysis section increases the utility of the conversation record by transforming raw dialog data into meaningful information.
This can include automatically deriving summaries, measuring sentiment, extracting key topics, and identifying action items.
Such insights are pivotal in generating business intelligence, facilitating quality control, and supporting various applications where actionable information from conversations is crucial.

Analysis data represents a significant privacy consideration as it often contains processed personal information that may reveal insights about individuals beyond what is explicitly stated in the original conversation.
This includes inferred characteristics, behavioral patterns, emotional states, and other derived information that could be considered personal data under privacy regulations.
The vCon creator and processors must ensure that any analysis performed complies with applicable privacy laws and that data subjects are informed about what analysis is being conducted on their data.

The "Right to know" principle is particularly important in the analysis section, as individuals have the right to understand what information is being derived from their conversations and how it is being used.
This includes transparency about what types of analysis are being performed, what insights are being generated, and how those insights are being applied. Organizations processing vCons must provide clear information about the analytical processes being applied to conversation data, including the purposes of analysis, the types of insights being generated, and how those insights may be used to make decisions about individuals.

The analysis section enables organizations to extract value from conversations while maintaining accountability for how personal information is processed.
By clearly documenting what analysis has been performed and linking it back to specific dialog segments, the analysis section supports compliance with data subject rights requests, enables audit trails for analytical processes, and provides transparency about how conversation data is being transformed into business intelligence.

## Relationships between vCons

vCons can be related to other vCons through three distinct mechanisms: redaction, appending, and grouping. These relationship types are mutually exclusive, meaning a vCon can use only one of these mechanisms at a time. Each relationship type serves different purposes in the conversation lifecycle and enables specific use cases while maintaining data integrity and provenance.

### Redacted vCons

Redaction enables data minimization, a fundamental principle of privacy protection. A redacted vCon creates a new version with reduced information while maintaining a verifiable reference to the original, more complete version. This mechanism allows organizations to share conversation data appropriate to different contexts and authorization levels while preserving the ability to verify the authenticity and accuracy of the redaction.

When a vCon is redacted, each piece of data from the original version is handled in one of three ways: removed entirely from the redacted version, copied with partial redaction applied, or copied unchanged. For data that is completely removed from JSON arrays, empty placeholders should be created to maintain consistent array indices across versions. This structural preservation ensures that references and indices remain valid even as content is removed.

The redacted vCon contains a Redacted Object that references the unredacted or less-redacted prior version through its UUID. The reference may include a URL for accessing the original version and a content hash for integrity verification. Access to the unredacted version must be strictly controlled to protect the sensitive information that was removed. The entity creating the redaction should sign the redacted vCon to attest to the accuracy and appropriateness of the redaction performed.
When shared, the referenced unredacted version should be encrypted.

Common redaction scenarios include removing personally identifiable information to enable broader analysis, creating versions appropriate for different security clearances or authorization levels, producing versions suitable for sharing with third-party processors who need limited information, and generating versions that comply with specific regulatory requirements for data minimization.

### Appended vCons

Appending addresses the challenge of evolving immutable conversation records. Once a vCon has been cryptographically signed or encrypted, any modification would invalidate the signature. When additional information needs to be added to such a vCon, or when existing information needs to be corrected or updated, a new vCon instance version must be created.

An appended vCon is a deep copy of the prior version with amendments or additions. It contains all the data from the referenced prior version, with the exception of any data that has been specifically amended. This approach maintains the complete conversation record while enabling evolution and enhancement over time. The appended vCon references the prior version through an Appended Object containing the prior version's UUID, and optionally its URL and content hash.

The appending mechanism enables several important use cases. Analysis results can be added to a conversation record that was signed when initially captured. Corrections can be made to metadata or party information while preserving the original signed version. Additional conversational data from later stages of the conversation can be incorporated. Multiple processing stages can each contribute their additions while maintaining a clear chain of versions. Each stage can sign its version, creating an auditable history of how the conversation record evolved.

This approach balances two competing needs: the requirement for immutability to maintain integrity and trust, and the practical necessity to enhance and evolve conversation records as additional information becomes available or processing occurs.

### Group vCons

Grouping enables the aggregation of multiple separate vCon instances into a single logical conversation. The scope and boundaries of a conversation are defined by the observer and the business context. A single conversation might consist of a quick text exchange, a simple two-party call, an evolving group chat, a class lecture with questions and answers, a multi-stage interaction evolving from web chat to phone call to video conference, a series of related calls about the same support incident, or a sequence of periodic meetings on a common topic.

When these components of a conversation are captured in separate vCons, perhaps because they occurred in different communication silos, different security domains, or at different times when each was individually signed, the group mechanism allows them to be treated as a unified conversation. A vCon with a group array aggregates these separate instances, with each Group Object referencing one component vCon through its UUID, URL, and content hash.

The group mechanism differs from appending in a fundamental way: appended vCons create deep copies containing all prior data in a single structure, while grouped vCons maintain references to separate, independent vCon instances. This distinction matters for storage efficiency, security boundaries, and processing patterns. Groups preserve the independence and individual signatures of component vCons while expressing their logical relationship. This is particularly valuable when component conversations occurred across organizational boundaries, involved different sets of parties, or required separate security treatments while still forming part of a larger conversational context.

## Trust and Integrity

Trust in conversation data requires mechanisms to verify authenticity, detect tampering, and establish provenance across organizational boundaries. The vCon framework provides several conceptual approaches to building and maintaining trust throughout the conversation lifecycle.

**Chain of custody** refers to the documented sequence of entities that have possessed, processed, or modified a vCon. In legal, regulatory, and business contexts, establishing an unbroken chain of custody is essential for demonstrating that conversation data has been properly handled and has not been corrupted or altered inappropriately. vCons support chain of custody through version references that link related vCons, timestamps that record when changes occurred, cryptographic signatures that identify who made changes, and metadata that documents the processing history. When a vCon passes between organizations or crosses trust boundaries, maintaining chain of custody becomes critical for both parties to demonstrate proper data handling.

**Tamper evidence** is the ability to detect whether a vCon has been modified after creation or signing. Unlike tamper-proofing, which attempts to prevent modification entirely, tamper evidence focuses on making any unauthorized changes detectable. Cryptographic signatures provide the primary mechanism for tamper evidence in vCons. When a vCon is signed, any subsequent modification to the signed content will invalidate the signature, immediately revealing that tampering has occurred. This property is essential for regulatory compliance, legal proceedings, and audit scenarios where the integrity of conversation records must be demonstrable. The immutability provided by signing also supports the creation of verifiable audit trails.

**Trust boundaries and security domains** represent the organizational or technical perimeters within which data can flow freely, beyond which additional controls and verification become necessary. A vCon might be created within one security domain such as a contact center, transferred to a second domain such as a cloud transcription service, and ultimately stored in a third domain such as a long-term archive. Each boundary crossing represents a point where trust must be explicitly established through authentication of the receiving party, verification of the vCon's integrity, documentation of the transfer for audit purposes, and potentially transformation of the vCon such as through redaction or encryption. Understanding and properly managing trust boundaries is essential for organizations operating distributed systems or engaging external service providers for conversation processing.

**Attestation** is the act of making a verifiable claim about a vCon or its contents. Different entities in the vCon lifecycle may attest to different aspects: a conversation platform might attest that a dialog was captured accurately, a transcription service might attest to the quality of its analysis, a controller might attest that proper consent was obtained, or a redactor might attest that personal information was removed according to specified rules. Attestations can be embedded in vCons through signatures, documented in external transparency services, or recorded through standardized extension mechanisms. The ability to make and verify attestations enables distributed systems to operate with appropriate levels of trust while maintaining independent verification capabilities.

## Appended Use Cases

A vCon will often evolve over time.
It is not always created with all of its metadata, conversation media, attachments, and analysis at once.
There are several reasons for this:

- Different components of the vCon may be produced by different application platforms or entities.
- The vCon may pass across multiple trust boundaries during its lifecycle, with entities on either side contributing content.
- Each of these entities may wish to sign the vCon to attest to its integrity or to the authenticity of their contributions.

Once a vCon has been signed, it becomes immutable.
Any modification will invalidate the signature.
To address this, a new vCon can be created containing the updated or additional content.
This new vCon can reference the previously signed version, preserving the integrity of the earlier state while allowing the overall conversation record to evolve.

This approach can also be applied even when a vCon is unsigned, for scenarios where maintaining a historical snapshot is important.
For example, an application may wish to preserve a point-in-time representation of the vCon at a significant stage in its lifecycle.

There are two competing requirements in this use case:

- **Ease of use and access to the latest version of the vCon**
- **Data size minimization and normalization**

For ease of use, it is often desirable to work with a fully composed vCon that contains all prior and newly added or updated content.
This has sometimes been referred to in vCon discussions as a "deep copy." Such a vCon requires no special handling, redirection, or reconstruction.
It contains all relevant information in a single, self-contained structure.

However, this approach introduces duplication and increases document size.
To address concerns around efficiency and data normalization, a more compact representation using *patches* or *incremental updates* may be preferred.
This method allows changes to be recorded relative to earlier versions, reducing redundancy.
Additionally, it enables labeling or referencing specific stages in the vCon's lifecycle, offering a flexible way to manage changes.
In vCon discussions, this method has been referred to as representing *incremental changes*.

# Security Considerations

The JSON form of a vCon is contained in a JSON object in one of three forms:

* unsigned - for internal use or trusted environments where data integrity and authenticity verification are not required
* signed - for scenarios requiring data integrity verification and authenticity confirmation without encryption, enabling tamper detection while maintaining readability
* encrypted - for sensitive conversations requiring confidentiality protection, ensuring that only authorized parties with proper decryption keys can access the conversation content

## Defense in Depth

Securing conversation data requires multiple layers of protection rather than relying on any single mechanism. Defense in depth recognizes that no security control is perfect, and that comprehensive protection comes from combining complementary safeguards at different levels.

For vCons, defense in depth might include cryptographic protection through signing and encryption of the vCon itself, transport security using TLS or similar protocols when vCons are transmitted between systems, storage security including encryption at rest and access controls where vCons are persisted, application security that validates vCon content and enforces business rules before processing, and organizational security through policies, training, and audit procedures that govern how vCons are handled. Each layer provides protection even if another layer is compromised, creating resilience against both technical attacks and operational failures.

The choice of which security layers to employ depends on the sensitivity of the conversation content, the threat model for the specific deployment, regulatory requirements applicable to the data, and the trust relationships between entities handling the vCon. Organizations should conduct risk assessments to determine appropriate security measures for their specific use cases.

## Encryption at Rest and in Transit

Encryption serves different purposes at different stages of the vCon lifecycle, and understanding when each type applies helps ensure appropriate protection.

**Encryption in transit** protects vCons as they move between systems. When a vCon is transmitted over a network, whether between internal services or to external partners, transport-layer encryption such as TLS prevents interception and eavesdropping. This is particularly important when vCons cross trust boundaries or traverse public networks. Transport encryption is typically mandatory for any transmission of conversation data containing personal information, and most privacy regulations require encryption in transit as a baseline security measure.

**Encryption at rest** protects stored vCons from unauthorized access. When vCons are persisted in databases, file systems, or object storage, encryption at rest ensures that even if storage media is compromised, the conversation content remains protected. The vCon format itself supports encryption through standard mechanisms, allowing individual vCons to be encrypted before storage. This enables fine-grained control where some vCons might be stored encrypted while others remain in readable form based on sensitivity levels.

The relationship between these encryption types and the vCon's own encryption format requires careful consideration. A vCon might be stored in encrypted form using the vCon encryption mechanism, placed in encrypted storage providing a second layer, and transmitted over encrypted channels providing a third layer. Alternatively, a signed but unencrypted vCon might rely solely on storage and transport encryption for confidentiality while the signature provides integrity protection.

## Access Control Principles

Access control determines who can read, modify, or delete vCons at various stages of their lifecycle. Effective access control for conversation data requires careful consideration of roles, permissions, and contexts.

**Role-based access control** maps permissions to organizational roles rather than individuals, simplifying management as personnel change. For vCons, relevant roles might include conversation participants who typically have rights to access their own conversations, contact center agents who need access to conversations they handle, supervisors who require access for quality assurance, analysts who process aggregate conversation data, and administrators who manage the vCon infrastructure. Each role receives the minimum permissions necessary for their function, following the principle of least privilege.

**Attribute-based access control** makes decisions based on properties of the vCon, the requestor, and the context. For example, access might be granted based on whether the vCon contains a specific party, whether adequate consent has been documented, how old the conversation is, what analysis has been performed, or where the access request originates. Attribute-based control provides flexibility for complex scenarios where simple role-based rules are insufficient.

**Audit logging** of access to vCons creates accountability and enables detection of inappropriate access patterns. Every access to conversation data should be logged with sufficient detail to support security investigations and regulatory compliance requirements. The immutable and signed nature of vCons can extend to audit logs, creating tamper-evident records of who accessed what conversation data and when.

# IANA Considerations

IANA considerations for vCon are defined in the vCon core specification.

--- back

# Acknowledgments
{:numbered="false"}

* Thank you to Daniel Petrie for making a concept real, for all the right reasons, and for the many projects we've shared over our careers.
* Thank you to Jonathan Rosenberg and Andrew Siciliano for their input to the vCon container requirements in the form of I-D: draft-rosenberg-vcon-cc-usecases.
* Thank you to Rohan Mahy for his help in exploring the CDDL schema and CBOR format for vCon.
* Thank you to Steve Lasker for formatting and spelling edits.
