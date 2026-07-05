---
name: privatenotes-testing-demo
description: |
  Testing, validation, and demo guidance for PrivateNotes Builder and generated Android apps. Use this skill when writing tests, demo data, README verification steps, or Kaggle video scripts.
---

# PrivateNotes Testing + Demo

## Testing priorities

Test the generated app behavior, not only helper functions.

MVP tests should cover:

- app config validation
- template rendering
- category generation
- create entry
- search entry
- filter by category
- delete entry
- repository mapping
- ViewModel state updates

## Builder backend tests

Use Python tests for:

```text
valid app_config is accepted
invalid package name is rejected
duplicate categories are normalized or rejected
template rendering creates expected files
generated README contains app name and categories
path traversal is blocked
```

## Android unit tests

Use fake repository tests for ViewModels.

Example test cases:

```text
EntryListViewModel shows entries from repository
Search query updates state
Category filter updates state
Delete action removes entry and shows snackbar
AddEntryViewModel rejects empty title
```

## Manual demo script

Use one generated app: FamilyVault.

Configuration:

```text
App name: FamilyVault
Categories: School, Baby, Housework, Travel, Health, Other
Features: create, list, search, filter, delete
Storage: local only
```

Demo entries:

```text
School: School picnic on Friday. Bring water bottle.
Baby: Buy diapers and wipes.
Travel: Pack passports for Amsterdam trip.
Housework: Clean induction hob.
Health: Book dentist appointment.
```

Demo flow:

1. Show builder input.
2. Show generated `app_config.json`.
3. Show generated Android project.
4. Build/run app in emulator.
5. Add a School note.
6. Add a Baby note.
7. Search for `picnic`.
8. Filter by `Baby`.
9. Delete an entry.
10. Open privacy screen showing local-only storage.

## Kaggle concept evidence

In README/video, explicitly show:

- ADK/multi-agent builder workflow
- MCP server tools for validation/rendering/build
- Antigravity usage with project skills
- security/privacy choices
- generated app builds and runs

## Definition of done

The MVP is done when:

- builder can generate one customized Android app from config
- generated app builds
- generated app supports create/list/search/filter/delete
- privacy screen exists
- README explains how to run
- video can show end-to-end generation and app usage
