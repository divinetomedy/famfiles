# FamFiles

A private, Apple-native family information reference app for storing, finding, and using important family records — birthdays, SSNs, passports, driver's licenses, health and auto/home insurance, frequent-flyer numbers, vehicle and home records, and the documents behind them.

FamFiles is designed to make capturing family information dramatically easier than maintaining a shared doc, while keeping the original source image or file alongside the structured data extracted from it.

## Two core interaction modes

1. **In-app browsing and management** — navigate the household, people, and records.
2. **Siri natural-language retrieval** — ask for information conversationally (e.g. "What is my SSN?") rather than through an in-app chat.

## Core concepts

- **Family** — a household-level container for people and shared records (home/auto insurance, memberships).
- **Person** — an individual family member with optional profile photo and associated records.
- **Record** — a structured collection of related fields (e.g. a health-insurance card with provider, plan, member ID, group number), optionally linked to source files.
- **Source artifact** — the original photo, PDF, or file the data was extracted from, preserved alongside the record.
- **Activity history** — a chronological log of additions and changes, for transparency.

## How intake works

When a photo or file is imported (camera, Photos, Files, Share Sheet, manual entry, or pasted text), FamFiles:

1. Saves the original source artifact.
2. Identifies the likely document type and extracts likely fields.
3. Identifies the associated person or household record.
4. Creates a new record or, on a high-confidence match, updates the existing one.
5. Logs the action in activity history.
6. Makes the new data immediately available in-app and via Siri.

## MVP scope

The first build is intentionally local-only to validate the product:

- **Platform:** native Swift, iPhone first, iPad where practical.
- **Storage:** local database and local file storage — no iCloud sync, no family sharing.
- **Security:** no encryption or biometric gate in MVP; sensitive and non-sensitive answers share the same design. Privacy, encryption, sync, sharing, and authentication are added in deliberate later phases.

Six visual moments are in scope for MVP: simple Siri answer, grouped-record Siri answer, family (home) view, person view, grouped/card record view, and the Share Sheet import flow.

## Product principles

- Make adding information dramatically easier than maintaining a Google Doc.
- Preserve the original source alongside structured data.
- Let high-confidence imports become usable immediately.
- Use Siri as the conversational interface — no in-app chat.
- Start local and simple; layer in privacy, encryption, sync, and sharing deliberately.
- Never make the user manually organize data the app can reliably infer.

## Repository contents

- [`famfiles product spec.md`](famfiles%20product%20spec.md) — the full product specification.
- [`FamFiles app design system/`](FamFiles%20app%20design%20system/) — design-system reference and assets.
