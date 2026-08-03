# Amazon Interactive Video Service (amazon-interactive-video-service)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Amazon Interactive Video Service (Amazon IVS) is a managed live streaming solution designed to provide interactive video experiences. It handles the operational complexity of live streaming so you can focus on building engaging applications.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/amazon-interactive-video-service/refs/heads/main/apis.yml)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - AWS, Live Streaming, Media, Video, Real-Time

## Timestamps

- **Created:** 2026-03-16
- **Modified:** 2026-04-19

## APIs

### AWS Amazon IVS API
The Amazon IVS API provides programmatic control over channels, stream keys, recordings, and playback keys for building interactive live streaming applications.

**Human URL:** [https://aws.amazon.com/ivs/](https://aws.amazon.com/ivs/)

#### Tags:

 - Live Streaming, Media, Video

#### Properties

- [Documentation](https://docs.aws.amazon.com/ivs/latest/APIReference/Welcome.html)
- [OpenAPI](openapi/amazon-ivs-openapi-original.yml)
- [GettingStarted](https://docs.aws.amazon.com/ivs/latest/userguide/getting-started.html)
- [Pricing](https://aws.amazon.com/ivs/pricing/)
- [FAQ](https://aws.amazon.com/ivs/faqs/)

## Common Properties

- [Portal](https://aws.amazon.com/ivs/)
- [Website](https://aws.amazon.com/ivs/)
- [Documentation](https://docs.aws.amazon.com/ivs/)
- [TermsOfService](https://aws.amazon.com/service-terms/)
- [PrivacyPolicy](https://aws.amazon.com/privacy/)
- [Support](https://aws.amazon.com/premiumsupport/)
- [Blog](https://aws.amazon.com/blogs/media/tag/amazon-interactive-video-service/)
- [GitHubOrganization](https://github.com/aws)
- [Console](https://console.aws.amazon.com/ivs/)
- [SignUp](https://portal.aws.amazon.com/billing/signup)
- [Login](https://signin.aws.amazon.com/)
- [StatusPage](https://health.aws.amazon.com/health/status)
- [Contact](https://aws.amazon.com/contact-us/)

## Features

| Name | Description |
|------|-------------|
| Low Latency Streaming | Deliver live video with sub-second latency for real-time interactivity. |
| Managed Infrastructure | AWS handles all the infrastructure complexity of live streaming at scale. |
| Recording and Playback | Automatically record live streams to S3 and generate playback URLs. |
| Chat Integration | Built-in chat messaging for interactive viewer experiences. |

## Use Cases

| Name | Description |
|------|-------------|
| Interactive Gaming Streams | Build gaming livestreams with viewer interaction and real-time overlays. |
| Virtual Events | Host virtual conferences, concerts, and events with large audiences. |
| Social Commerce | Enable live shopping experiences with interactive product displays. |

## Integrations

| Name | Description |
|------|-------------|
| Amazon S3 | Stores live stream recordings automatically for on-demand playback. |
| Amazon CloudFront | Distributes live streams globally with low latency. |
| AWS Lambda | Triggers automation based on stream state changes and events. |

## Artifacts

Machine-readable API specifications organized by format.

### OpenAPI

- [AWS Amazon IVS API](openapi/amazon-ivs-openapi-original.yml)

### JSON Schema

109 schema files covering key resources and operations.

### JSON Structure

109 JSON Structure files converted from JSON Schema.

### JSON-LD

- [Amazon Interactive Video Service Context](json-ld/amazon-interactive-video-service-context.jsonld)

### Examples

109 example JSON files generated from schemas.

## Capabilities

Naftiko capabilities organized as shared per-API definitions composed into customer-facing workflows.

### Shared Per-API Definitions

- [AWS Amazon IVS API](capabilities/shared/ivs.yaml) — operations for amazon interactive video service management

### Workflow Capabilities

| Workflow | APIs Combined | Tools | Persona |
|----------|--------------|-------|---------|
| [Live Streaming Management](capabilities/live-streaming-management.yaml) | Amazon Interactive Video Service | 8 | Developer, Media Engineer |

## Vocabulary

- [Amazon Interactive Video Service Vocabulary](vocabulary/amazon-interactive-video-service-vocabulary.yaml) — Unified taxonomy mapping resources, actions, workflows, and personas

## Rules

- [Amazon Interactive Video Service Spectral Rules](rules/amazon-interactive-video-service-spectral-rules.yml) — 14 rules across 6 categories enforcing Amazon Interactive Video Service API conventions

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
