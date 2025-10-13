<!-- regenerate: on (set to off if you edit this file) -->

# The vCon - Conversation Data Container - Overview

This is the working area for the IETF [VCON Working Group](https://datatracker.ietf.org/group/vcon/documents/) Internet-Draft, "The vCon - Conversation Data Container - Overview".

## What is vCon?

A **vCon** (Conversation Data Container) is a standardized JSON container for conversational data, analogous to how vCard standardizes contact information. It provides a unified format for capturing, storing, and exchanging conversation data across multiple communication channels including:

- Voice calls (PSTN, SIP, WebRTC)
- Video conferences
- Text messaging (SMS, MMS, web chat)
- Email threads
- And other communication modes

### Key Components

A vCon contains four major categories of data:

1. **Parties** - Identification of conversation participants
2. **Dialog** - The actual conversation content (audio, video, text)
3. **Analysis** - Derived insights (transcripts, translations, sentiment analysis)
4. **Attachments** - Supporting files and context (documents, consent records)

### Why vCon?

vCons solve critical challenges in conversation data management:

- **Interoperability**: Standardized format enables seamless data exchange between systems and service providers
- **Privacy & Compliance**: Built-in support for data minimization, consent management, and regulatory compliance (GDPR, CCPA, HIPAA)
- **Data Integrity**: Cryptographic signing and encryption capabilities ensure authenticity and tamper detection
- **Flexibility**: Supports inline or externally referenced media, versioning through redaction and appending

### Use Cases

- **Contact Centers**: Unified customer journey tracking across all communication channels
- **Healthcare**: HIPAA-compliant patient communication records with privacy controls
- **Emergency Services**: Comprehensive situational awareness and multi-agency coordination
- **Legal & Compliance**: Tamper-evident conversation records with chain of custody

## Document Links

* [Editor's Copy](https://ietf-wg-vcon.github.io/draft-ietf-vcon-overview/#go.draft-ietf-vcon-overview.html)
* [Datatracker Page](https://datatracker.ietf.org/doc/draft-ietf-vcon-overview)
* [Working Group Draft](https://datatracker.ietf.org/doc/html/draft-ietf-vcon-overview)
* [Compare Editor's Copy to Working Group Draft](https://ietf-wg-vcon.github.io/draft-ietf-vcon-overview/#go.draft-ietf-vcon-overview.diff)

## Related Resources

* [VCON Working Group Page](https://datatracker.ietf.org/group/vcon/documents/)
* [Mailing List](https://mailarchive.ietf.org/arch/browse/vcon/)
* [vCon Core Specification](https://datatracker.ietf.org/doc/draft-ietf-vcon-vcon-core/)
* [Python vCon Implementation](https://github.com/py-vcon/py-vcon)

## Contributing

See the [guidelines for contributions](https://github.com/ietf-wg-vcon/draft-ietf-vcon-overview/blob/main/CONTRIBUTING.md).

Contributions can be made by creating pull requests. The GitHub interface supports creating pull requests using the Edit (✏) button.

## Building the Draft

Formatted text and HTML versions of the draft can be built using `make`:

```sh
$ make
```

This will generate:
- `draft-ietf-vcon-overview.txt` - Plain text version
- `draft-ietf-vcon-overview.html` - HTML version

### Requirements

Building the draft requires specific tools to be installed. See [the setup instructions](https://github.com/martinthomson/i-d-template/blob/main/doc/SETUP.md) for details.

Common requirements include:
- `xml2rfc` - Primary RFC formatting tool
- `kramdown-rfc` - Markdown to XML converter
- Python 3.x with required packages

## Quick Start for Contributors

1. Fork and clone this repository
2. Make your changes to `draft-ietf-vcon-overview.md`
3. Run `make` to verify the document builds correctly
4. Submit a pull request with a clear description of your changes

## License

See [LICENSE.md](LICENSE.md) for licensing information.
