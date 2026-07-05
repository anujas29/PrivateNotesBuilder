---
name: privatenotes-android-template-architecture
description: |
  Android architecture for the generated local-first notes app. Use this skill when creating the Android template, adding modules, deciding package structure, wiring Gradle, or separating app, data, domain, and UI code.
---

# PrivateNotes Android Template Architecture

## Target stack

Use:

- Kotlin
- Jetpack Compose
- Room
- Koin
- Navigation Compose
- Kotlin Coroutines and Flow
- ViewModel with StateFlow
- version catalog for dependencies

Avoid unnecessary KMP complexity for the MVP unless the project already has it.

## Recommended simple module layout

For the MVP, prefer a compact Android app structure over excessive modularization:

```text
generated-app/
├── app/
│   └── src/main/java/<package>/
│       ├── MainActivity.kt
│       ├── PrivateNotesApp.kt
│       ├── di/
│       ├── data/
│       │   ├── database/
│       │   ├── entity/
│       │   ├── dao/
│       │   ├── mapper/
│       │   └── repository/
│       ├── domain/
│       │   ├── model/
│       │   ├── repository/
│       │   └── error/
│       ├── presentation/
│       │   ├── navigation/
│       │   ├── entries/
│       │   ├── search/
│       │   ├── settings/
│       │   └── components/
│       └── ui/theme/
```

Only split into Gradle modules if the repo already supports it or if the user explicitly asks.

## Feature areas

Use these package areas:

- `presentation.entries` for list, detail, add/edit/delete
- `presentation.search` for search and category filtering
- `presentation.settings` for privacy and delete-all-data actions
- `data.database` for Room database, DAO, and entities
- `data.repository` for repository implementation
- `domain.model` for `KnowledgeEntry`
- `domain.repository` for repository interface

## Generated app configuration

The builder should use an `app_config.json` like:

```json
{
  "appName": "FamilyVault",
  "packageName": "com.example.familyvault",
  "themeColor": "#3F51B5",
  "categories": ["School", "Baby", "Housework", "Travel", "Health", "Other"],
  "features": {
    "images": false,
    "analytics": false,
    "localLlm": false
  }
}
```

## Code generation rules

- All generated package names must be valid Kotlin/Android package names.
- Categories must be escaped safely and never inserted into code without sanitization.
- Use placeholders in templates rather than free-form code rewriting.
- Keep generated files deterministic so diffs are easy to review.
- The generated app must build without internet access after Gradle dependencies are resolved.

## Non-goals

Do not add authentication, networking, sync, accounts, or cloud storage to the generated app.
