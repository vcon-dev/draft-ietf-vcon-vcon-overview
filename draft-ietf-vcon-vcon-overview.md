---
title: "The vCon - Conversation Data Container - Overview"
abbrev: "vCon Overveiw"
category: fyi

docname: draft-ietf-vcon-vcon-overview-latest

submissiontype: IETF  # also: "independent", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
area: "ART"
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
  type: ""
  mail: "vcon@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/vcon/"
  github: "ietf-wg-vcon/draft-ietf-vcon-vcon-overview"
  latest: "https://ietf-wg-vcon.github.io/draft-ietf-vcon-vcon-overview/draft-ietf-vcon-vcon-overview.html"

author:
 -
    fullname: Daniel G Petrie
    organization: SIPez LLC
    email: dan.ietf@sipez.com

 -
    fullname: Thomas McCarthy-Howe
    organization: Strolid
    email: thomas.howe@strolid.com

normative:

  RFC3339:


informative:

TODO:  the following were normative in the container I-D.  Most can probably be deleted.

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

TODO:  end formerly normative references.  Many of the following informationaly references can probably also be deleted from this overview I-D

  CBOR: RFC8949

  CDDL: RFC8610

  ISOBMFF:
    target: https://www.iso.org/standard/83102.html
    title: "Information technology -- Coding of audio-visual objects -- Part 12: ISO base media file format"
    refcontent: ISO/IEC 14496-12:2022
    date: January 2022
    org: International Organization for Standardization

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
    author:
      org: ITU
      date: 1998

  PY-VCON:
    target: https://github.com/py-vcon/py-vcon
    title: "Python open source vCon command line interface, library and workflow server"

--- abstract

A vCon is the container for data and information relating to a real-time, human conversation.
It is analogous to a {{vCard}} which enables the definition, interchange and storage of an individual's various points of contact.
The data contained in a vCon may be derived from any multimedia session, traditional phone call, video conference, SMS or MMS message exchange, webchat or email thread.
The data in the container relating to the conversation may include Call Detail Records (CDR), call meta data, participant identity information (e.g. STIR PASSporT), the actual conversational data exchanged (e.g. audio, video, text), realtime or post conversational analysis and attachments of files exchanged during the conversation.
A standardized conversation container enables many applications, establishes a common method of storage and interchange, and supports identity, privacy and security efforts (see {{vCon-white-paper}})

--- middle

# Introduction

The generation of conversational data, contained in transcripts and multi-media files, is common in business, especially in customer facing organizations.
However, the storage, analysis and sharing of the data they contain is not currently a standard.
Standardizing a container for conversation data (vCon) has numerous advantages, and enables the management of the conversation's content.
Very often the system providing the communications service, the consumer and/or owner of the communications data and the communications analysis services are distinct systems and in many case separate business entities.
The point of a vCon is to provide a standard means of exchanging communications data between these systems and services.
The use of vCons can ease service integration by using a common container and format for enterprise communications.
A vCon becomes the standardized input to communication analysis tools and machine learning and categorization.
For a sales lead organization, a vCon can be the container of assets sold to sales teams.
For conversations of record, the vCon can be a legal instrument.
For machine learning efforts, vCons can track what information was used in the training of models, so that as the result of a customer requested deletion of their data, the affected models can be identified.

## What's in a vCon?

A vCon contains four major categories of data: metadata , dialog , analysis and attachments.
The metadata portion allows for an expanded set of data from a typical call detail record ([CDR]), with identifications of the participants or parties to the conversation, references to related or earlier versions of the vCon.
The dialog portion contains a set of multimedia and media type elements, each representing the actual, physical conversation in it's original media form: text, audio or video.
The analysis portion contains data derived from the metadata and dialog portions, intended to carry items like transcripts, translations, summaries, text to speech, sentiment analysis and other semantic tagging.
Finally, the attachment portion contains any other documents, such as slide deck or sales lead information, which provides context and support for the conversation itself.
The vCon may also container integrity checking information such as the issuer of the vCon and tamper-proof features such as signatures.

A vCon acts as the definition of the conversation, and are created by systems during and after the conversation itself.
Some communication modes, like SMS texting, lack natural session boundaries and require explicit definition.
vCons may have two or more parties involved, but at least one should be a human.
For instance, an interaction between a bot and a human is an appropriate scope for vCons, but a conversation between two bots would not.

Due to the size and complexity of some portions of a vCon, both inline and externally referenced dialog, analysis, attachments and other vCon reference assets are supported.
For instance, vCons may reference a video conference media recording as an external URL with an accompanying content hash of the contents to detect tampering.
Alternatively, vCons may directly contain the media of the entire dialog internally, keeping the conversation in one place, and optionally encrypted.

vCons are designed to be a digital asset, versioned and signed.
For instance, different versions of vCon may arise due to redaction (e.g. for PII or other reasons), added analysis or the addition of other content.
In the metadata, vCons contain the unique ID of the parent vCon, such that they may be traversed while maintaining their data integrity and provenance.

## Use Cases and Requirements

### Contact Center Use Case

### Messaging Use Case

### ECRIT Use Case


May of the initial set of use cases for vCons are expected to be in the interchange between front end and back end application and lower layers of the network stack, critical for enablement of analysis of conversations.
It is expected that JavaScript handling of vCons in the front end and RESTful interfaces and back end platforms will be used for operations and manipulation of vCons.
Many media analysis services which will be used with vCons, such as transcription, already use JSON based interfaces.
For this reason, JSON has been chosen for the initial format binding of vCons and the scope of this document.
Other bindings (e.g. [CBOR] or [CDDL]) may be consider for vCon in the future in other documents.

An outline of the vCon requirements derived from the explored use case follows:

* Standardize container for conversational data exchange

* Consolidation of data and information for a conversation

* Multiple modes of communication, changing over time

* Snapshots of conversation during or once completed along with analysis

* Ease of integration of services and analysis

* Better organize conversational data so that it can be handled in a consistent, privacy safer means

* Immutable

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

* Methods of redaction of text, audio or video media

* Validation of redactions or appended data beyond the signature of the domain making the changes to the conversational data (e.g. Merkle tree like redactions)

* Standardization of analysis data formats or file media types

# Conventions and Definitions

{::boilerplate bcp14-tagged}

## Terminology

* analysis - analysis, transformations, summary, sentiment, or translation typically of the dialog data

* conversation - an exchange of communication using text, audio or video medium between at least one human and one or more bots or humans

* de-identification - removal of all information that could identify a party in a conversation.  This includes PII as well as audio and video recordings.  Voice recordings might be re-vocalized with a different speaker.

* dialog - the captured conversation in its original form (e.g. text, audio or video)

* encrypted form - encrypted JWE document with the JWS signed vCon form contained in the ciphertext

* file - a data block either included or referenced in a vCon

* object - JSON object containing key and value pairs

* parameter - JSON key and value pair

* party - an observer or participant to the conversation, either passive or active

* payload - the contents or bytes that make up a file

* PII - Personal Identifiable Information

* PII masked - may include voice recordings, but PII is removed from transcripts and recordings (audio and video).

* vCon - container for conversational information

* vCon instance - a vCon populated with data for a specific conversation

* vCon instance version - a single version of an instance of a conversation, which may be modified to redact or append additional information  forming a subsequent vCon instance version

* vCon syntax version - the version for the data syntax used for form a vCon

* signed form - JWS signed document with the unsigned vCon form contained in the payload


## Inline Files

## Externally Referenced Files

# vCon JSON Object

The JSON form of a vCon is contained in a JSON object in one of three forms:

* unsigned
* signed
* encrypted


### uuid

### parties

### dialog

### attachments

### analysis

### redacted

~~~
{::include redacted-vcon-tree.ans}
~~~
{: #diagram1 title="redacted vCon object tree"}

### appended

### vCon groups


# Security Considerations

## Signing Externally Referenced Files


## Signed Form of vCon Object


## Encrypted Form of vCon Object


# IANA Considerations


# Non-Upward Compatible Changes to the vCon Container



--- back


# Acknowledgments
{:numbered="false"}

* Thank you to Thomas McCarthy-Howe for inventing the concept of a vCon and the many discussions that we had while this concept was developed into reality.
* Thank you to Jonathan Rosenberg and Andrew Siciliano for their input to the vCon container requirements in the form of I-D: draft-rosenberg-vcon-cc-usecases.
* Thank you to Rohan Mahy for his help in exploring the CDDL schema and CBOR format for vCon.
* Thank you to Steve Lasker for formatting and spelling edits.

