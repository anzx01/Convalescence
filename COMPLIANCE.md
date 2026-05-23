# Compliance Checklist

This checklist is for publishing and planning review. It is not legal advice.

## Repository Publication

- [x] No source code dependencies or vendored third-party code are currently
  included.
- [x] No production user data, database dumps, API keys, app secrets, access
  tokens, private keys, or real service endpoints were found in the repository
  scan.
- [x] Local assistant/tool configuration is excluded from publication.
- [x] The repository uses an "All Rights Reserved" copyright notice. This means
  the public can read the repository if it is public on GitHub, but no reuse
  rights are granted unless the owner gives separate written permission.
- [ ] If the owner wants others to freely use or contribute to the documents,
  replace the current license with a suitable open-source/content license.

## Medical And Health Positioning

- [ ] Product copy must state clearly that the product is a health-management
  reminder tool only.
- [ ] Do not provide diagnosis, treatment plans, prescription services, dosage
  changes, medication conflict conclusions, emergency triage, or claims that the
  product can prevent or cure disease unless the required medical qualifications
  and approvals are obtained.
- [ ] Require users to follow physician instructions for medication,
  rehabilitation, follow-up visits, and emergency handling.
- [ ] Health content, medication examples, thresholds, reminders, and
  rehabilitation tasks must be reviewed by qualified medical professionals
  before release.
- [ ] If future versions include remote consultation, electronic prescription,
  drug delivery, insurance use, hospital HIS integration, or doctor-side
  services, perform a separate legal and medical qualification review.

## Personal Information Protection

The product may process sensitive personal information, including health and
medical information. Before production use:

- [ ] Publish a privacy policy and user agreement before collecting data.
- [ ] Provide a personal information collection list covering purpose, method,
  scope, storage period, storage location, processor, sharing recipient, and
  user rights.
- [ ] Collect only data that is necessary for the selected product version.
- [ ] Obtain separate consent before processing sensitive personal information.
- [ ] Obtain separate consent before sharing patient data with family members,
  hospitals, cloud vendors, SMS providers, analytics tools, or AI services.
- [ ] Provide user access, correction, deletion, export, account cancellation,
  and consent-withdrawal flows.
- [ ] Define data retention periods and deletion rules.
- [ ] Avoid collecting precise location, ID numbers, medical images, discharge
  summaries, or contact lists unless a specific feature requires them.
- [ ] Encrypt data in transit and protect stored sensitive data with access
  controls, audit logs, backup controls, and least-privilege operations.
- [ ] Review requirements for minors or elderly users who may need guardian or
  family assistance.

## WeChat Mini Program Review

- [ ] Choose the correct service category in the WeChat Mini Program console and
  prepare required qualifications for medical/health-related categories.
- [ ] Configure the Mini Program privacy protection guide in the official
  console and keep it consistent with in-app behavior.
- [ ] Request only necessary APIs and permissions. Do not request location,
  background modes, camera, album, microphone, or file permissions unless a
  concrete feature requires them.
- [ ] Subscription messages must be user-initiated and scenario-specific.
- [ ] Server domains must use HTTPS and meet filing/registration requirements
  where applicable.
- [ ] Keep medical claims, screenshots, app descriptions, and template messages
  consistent with "health reminder only" positioning.

## Third-Party And Content Rights

- [ ] Use only self-created icons, screenshots, designs, diagrams, and images, or
  assets with explicit commercial/publication permission.
- [ ] Keep a source and license record for every asset added later.
- [ ] Do not copy substantial text from official guidelines, platform rules, or
  vendor documents into the repository. Link to official sources and summarize
  in your own words.
- [ ] Verify licenses before adding code, UI libraries, templates, fonts,
  datasets, or medical content.

