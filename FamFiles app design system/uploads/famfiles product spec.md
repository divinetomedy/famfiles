# FamFiles — Product Spec

## Product

FamFiles is a private, Apple-native family information reference app for storing, finding, and using important family records.

Examples include birthdays, SSNs, passports, driver’s licenses, health insurance, auto insurance, home insurance, frequent-flyer numbers, vehicle records, home records, and related documents.

The product has two core interaction modes:

1. **In-app browsing and management**
2. **Siri-based natural-language retrieval and simple updates**

The app should feel warm and lightweight at the family level, while making sensitive information easy to access and eventually highly secure.

---

# Product principles

- Make adding information dramatically easier than maintaining a Google Doc.
- Preserve the original source image, file, or document alongside structured extracted data.
- Let newly imported high-confidence data become usable immediately.
- Make Siri the conversational interface; do not build an in-app chat experience.
- Start local and simple.
- Add privacy, encryption, sync, and family-sharing capabilities in deliberate phases.
- Never make the user manually organize data when the app can infer structure reliably.

---

# Core data concepts

## Family

A household-level container for people and shared records.

Examples:
- Home insurance
- Auto insurance
- Shared utility or membership information

## Person

An individual family member with optional profile photo and associated records.

Examples:
- SSN
- Passport
- Driver’s license
- Health insurance member information
- Frequent-flyer numbers
- Birthday

## Record

A structured collection of related information, optionally associated with one or more source files.

Examples:
- Passport
- Health-insurance card
- Auto-insurance policy
- Driver’s license
- Home-insurance policy

A record may contain multiple related fields.

Example health-insurance record:
- Insurance provider
- Plan name
- Subscriber
- Group number
- Member ID
- Customer-service phone number
- Insurance-card image

## Source artifact

The original image, PDF, file, or imported material from which information was extracted.

Examples:
- Passport photo
- Insurance-card photo
- PDF policy document
- Screenshot
- File imported through Share Sheet

## Activity history

A chronological log of additions and changes.

Examples:
- “Tom’s passport added from photo.”
- “Mercer’s health-insurance member ID updated.”
- “Home-insurance policy imported.”
- “Scarlet’s birthday added manually.”

MVP history exists primarily for transparency and testing. It is not yet a complete version-control system.

---

# MVP

## MVP goal

Allow one person to begin using FamFiles meaningfully at home to:

- Add family information from photos, files, and manual entry.
- Browse people and records.
- Use Siri to retrieve information.
- See whether information was added or updated correctly.
- Preserve source imagery/files.
- Automatically update current values when the app confidently recognizes a matching record.

MVP is intentionally local-only and does not yet require cloud sync, family sharing, deletion workflows, or authentication.

---

## MVP platform

- Apple-only.
- Native Swift app.
- iPhone first.
- iPad support where practical.
- Local database and local file storage only.
- Siri and App Intents supported for defined retrieval intents.

---

## MVP storage

- Data lives locally on the user’s device.
- Source images and files are stored locally with the app.
- No iCloud sync.
- No family sharing.
- No backup/recovery guarantees beyond normal device backup behavior.
- No explicit encryption or biometric gate requirements in MVP.

This is a product-validation build, not yet the final privacy/security architecture.

---

## MVP intake methods

### Supported

- Take photo with camera
- Select image from Photos
- Import file
- Use Share Sheet from Photos, Files, Mail, Safari, or other compatible apps
- Manual entry
- Paste text

### Import flow

When a user sends an image or file to FamFiles:

1. The app saves the original source artifact.
2. The app identifies the likely document type.
3. The app extracts likely fields.
4. The app identifies the likely associated person, people, or family-level record.
5. The app creates a new record or updates an existing one.
6. The app records the action in activity history.
7. The new current data becomes immediately available through the app and Siri.

---

## MVP automatic updates

When an imported document produces a high-confidence match to an existing record, FamFiles automatically updates the current record.

Example:

1. A new passport photo is sent through the Share Sheet.
2. FamFiles identifies it as Tom’s passport.
3. The app extracts passport number and expiration date.
4. The app updates Tom’s current passport record.
5. The app preserves the imported image.
6. The app records the update in activity history.
7. A Siri request immediately returns the new passport number.

For MVP, “high confidence” should use reasonable matching signals where available:

- Associated person selected by the user
- Matching name
- Matching date of birth
- Matching document type
- Existing linked record
- High OCR confidence

Low-confidence handling is deferred to a later version.

---

# MVP visual design scope

Only these six visual moments are required for MVP design.

## 1. Siri answer result — simple

Example:

> “What is my SSN?”

Purpose:
- Return one clear answer.
- Allow copying.
- Link into the relevant record if needed.

Required content:
- Person name and optional profile photo
- Record type
- Hero answer
- Copy action
- Source artifact thumbnail where useful
- Open-record action

Example structure:

- Tom
- Social Security Number
- 123-45-6789
- Copy
- View record

This same design pattern applies to simple answers such as:

- Passport number
- Passport expiration date
- Driver’s-license number
- Birthday
- Frequent-flyer number

---

## 2. Siri answer result — grouped record

Example:

> “What is Mercer’s health insurance?”

Purpose:
- Return a compact summary of multiple related fields from one record.
- Let the user copy useful individual fields.
- Provide access to the source card/image and full record.

Required content:
- Person name and optional profile photo
- Record type
- Hero answer
- Related fields
- Copy actions for relevant fields
- Source artifact thumbnail
- Open-record action

Example structure:

- Mercer
- Health Insurance
- Premera Blue Cross
- Member ID: XXXXXXXX · Copy
- Group Number: XXXXXXXX · Copy
- Subscriber: Scarlet
- View insurance card
- Open record

This same pattern applies to:

- Auto-insurance policies
- Home-insurance policies
- Passport records
- Driver’s-license records
- Family travel records
- Membership or account records

Sensitive and non-sensitive answers use the same basic visual design in MVP. Authentication is added later.

---

## 3. Main app — family view

Purpose:
- Act as the home screen.
- Make the household easy to navigate.
- Make adding information obvious.
- Surface recent activity.

Required content:
- Family or household title
- Family-member cards with optional profile photos
- Household/shared-record entry point
- Prominent Add button
- Recent activity section

Example sections:

- Family members
  - Tom
  - Scarlet
  - Mercer
  - Winnie
  - August
- Household
  - Home insurance
  - Auto insurance
- Recent activity
  - “Tom’s passport updated”
  - “New health-insurance card added”
  - “Scarlet’s frequent-flyer number added”

This is not a chat screen and does not include in-app search.

---

## 4. Main app — person view

Purpose:
- Let the user browse everything associated with one person.

Required content:
- Profile photo
- Person name
- Key record categories
- Current records
- Add-information action
- Activity/history preview

Suggested categories:

- Identity
- Health
- Travel
- Insurance
- Memberships
- Other

Example records:

- Passport
- Driver’s license
- Social Security number
- Health-insurance card
- Frequent-flyer accounts
- Birthday

---

## 5. Main app — grouped/card record view

Purpose:
- Show a single multi-field record and its original source image/file.

Example:
- Health-insurance card
- Passport
- Auto-insurance policy
- Home-insurance policy

Required content:
- Record title
- Associated person or household
- Hero information
- Related structured fields
- Copy actions
- Original source artifact
- Edit action
- Activity/history for the record

Example health-insurance record:

- Mercer’s Health Insurance
- Premera Blue Cross
- Member ID
- Group Number
- Subscriber
- Customer-service phone number
- Insurance-card image
- Activity:
  - Added from image
  - Updated from new card image

For MVP, this is not yet a full version-history view. It shows a simple record-level activity log and retained source artifacts.

---

## 6. Share Sheet

Purpose:
- Make importing a photo, document, screenshot, or file feel nearly effortless.

Required states:

### Share Sheet destination

FamFiles appears as an available destination from:

- Photos
- Files
- Mail
- Safari
- Other compatible apps

Suggested label:

> Add to FamFiles

### Import processing

Required content:
- Source preview
- “Reading document…” state
- Detected document type
- Detected associated person or family-level match
- Extracted key fields where useful

Example:

- Passport detected
- Likely belongs to Tom
- Passport number extracted
- Expiration date extracted

### Successful update

Required content:
- Clear confirmation
- Person or household association
- Record updated or created
- Source image preview
- View record action

Example:

> Tom’s passport updated  
> New passport number and expiration date saved.  
> View record

### Ambiguous import

MVP does not need a sophisticated low-confidence system.

At minimum, when the app cannot reasonably identify a person or record, it should ask the user to choose:

- Which person does this belong to?
- Is this a new record or an update to an existing record?

---

# MVP Siri capabilities

## Read via Siri

Examples:

- “What is my SSN?”
- “What is Mercer’s health insurance?”
- “What is Tom’s passport number?”
- “When does Scarlet’s passport expire?”
- “What is our home-insurance policy number?”
- “What is Winnie’s birthday?”

Siri responses should use either:

- Simple answer result
- Grouped-record result

Siri should return current local app data.

---

## Write via Siri

MVP may support only simple structured updates, if straightforward.

Examples:

- “Add Mercer’s birthday as May 12.”
- “Update Tom’s passport expiration date to March 14, 2034.”
- “Add Scarlet’s frequent-flyer number.”

All write actions should include a confirmation step.

Complex document capture and review remain in the app or Share Sheet flow.

---

# MVP exclusions

The following are explicitly out of scope for MVP:

- iCloud sync
- Paid plans
- Family sharing
- Multiple devices
- User roles and permissions
- Biometric authentication
- Sensitive-field masking
- Encryption guarantees beyond normal device/platform protection
- Trash and permanent deletion
- Full version history
- Restore prior version
- Low-confidence extraction workflow
- Manual verification status
- Ownership transfer
- SMS access
- In-app chat
- In-app search
- AI-generated summaries or reasoning
- External AI processing of vault data

---

# V2 — Security, privacy, deletion, and versioning

## Goal

Turn FamFiles into a private personal vault suitable for sensitive identity and family information.

## Includes

- Local encrypted database
- Encrypted source-file storage
- Face ID / Touch ID / device-passcode protection
- Re-authentication before revealing or copying highly sensitive values
- Sensitive-field masking
- Trash
- Permanent deletion with confirmation
- Full version history
- Version comparison
- Restore prior version
- More complete audit/activity history
- Privacy controls
- No advertising, data resale, or model training on vault data

## Siri changes

- Sensitive Siri requests require authentication.
- Sensitive Siri result cards use the same visual design as MVP but only reveal data after authentication.
- Copying highly sensitive values may require re-authentication.

---

# V3 — Paid Family Vault and sharing

## Goal

Enable encrypted backup, multi-device access, and family collaboration.

## Includes

- Paid iCloud sync
- Encrypted cloud backup
- Multiple-device sync for the Owner
- Invitation-based family sharing
- One technical Vault Owner
- Family Admin UI for parents
- Roles:
  - Owner
  - Admin
  - Editor
  - Viewer
  - Restricted Child
- Category-level and record-level permissions
- Shared activity history
- Family notifications for meaningful changes

## Ownership model

- One technical Owner hosts the canonical cloud vault.
- Invited members access the shared vault through their Apple IDs.
- The UI may present multiple adults as Family Admins.
- The system still retains one technical owner underneath.

---

# V4 — Confidence handling and manual verification

## Goal

Make automatic extraction more trustworthy and understandable as the vault grows.

## Includes

- Explicit extraction-confidence model
- Low-confidence import review
- Conflicting-data resolution
- Duplicate-document detection
- Manual verification status
- Field-level provenance
- Suggested verification prompts
- Ability to indicate:
  - Manually verified
  - Automatically extracted
  - Imported as provided
  - Needs attention

Example future answer:

> “Tom’s passport number is X. Updated from a passport image on June 20, 2026 and not yet manually verified.”

---

# V5 — Ownership, recovery, and long-tail features

## Goal

Handle long-term family-vault needs and edge cases.

## Includes

- Vault ownership transfer
- Owner recovery flow
- More sophisticated family access controls
- Child-specific experiences
- Emergency-access planning
- Export/import tools
- Record-expiration reminders
- Renewal workflows
- More robust document matching
- More advanced source-document processing
- Optional integrations
- Possible SMS or iMessage access, with limited disclosure and explicit security constraints

---

# Future privacy direction

The intended long-term security posture is:

- Local-first encrypted vault
- Encrypted source documents
- Private on-device AI processing where possible
- No external AI access to source documents or secret values without explicit consent
- Paid encrypted iCloud sync
- Invitation-based family sharing
- Strong authentication for sensitive access
- No advertising, tracking, resale, or training on private vault data
