---
name: privatenotes-project-context
description: |
  Project context, scope, constraints, and non-goals for PrivateNotes Builder. Use this skill whenever planning, scoping, naming, writing README content, creating demo flows, or deciding whether a feature belongs in the MVP.
---

# PrivateNotes Builder Project Context

## One-line product definition

PrivateNotes Builder is an agent-assisted system that generates a local-first Android personal knowledge app with custom categories, note creation, listing, search, filtering, and deletion.

## MVP scope

The generated app must support:

- custom app name
- custom categories, such as School, Housework, Baby, Travel, Health, Other
- create entry
- list/display entries
- entry detail screen
- keyword search over title/body/tags
- filter by category
- delete entry
- local Room database
- no login
- no cloud sync
- privacy/settings screen explaining local-only storage

## Roadmap only; do not build in MVP unless explicitly requested

- local LLM
- OCR
- image upload
- analytics
- calendar integration
- contacts integration
- notifications
- backup/sync
- Play Store release
- rich text editor
- biometric lock

## Capstone framing

The capstone is not only a notes app. The main project is an app-generation workflow:

1. User describes the private app they want.
2. Builder extracts app name, categories, fields, privacy mode, and features.
3. Builder generates a customized Android project from a template.
4. Generated app runs locally on Android.

## Default generated app example

App name: FamilyVault  
Categories: School, Baby, Housework, Travel, Health, Other  
Features: create, list, search, filter, delete  
Storage: local only

## Decision rules

- Prefer boring, buildable, reliable MVP features over impressive but unstable features.
- Keep generated code simple and readable.
- Do not add cloud services unless the user explicitly asks.
- Do not add local LLM/OCR to MVP; document them as roadmap.
- When uncertain, choose privacy-preserving defaults.
