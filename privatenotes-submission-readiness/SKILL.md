---
name: privatenotes-submission-readiness
summary: Kaggle submission, attribution, and demo-readiness guidance.
description: |
  Submission-readiness guidance for the Kaggle AI Agents capstone. Use this skill when writing README sections, attribution, demo scripts, limitations, roadmap, or evidence for required concepts.
---

# PrivateNotes Submission Readiness

## Submission positioning

Describe the project as:

```text
PrivateNotes Builder is an ADK-based agent-assisted system that generates a local-first Android personal knowledge app with custom categories, local note creation, listing, search, filtering, and deletion.
```

Do not describe it as only a notes app. The capstone contribution is the builder workflow that creates a personalized Android app.

## Required evidence checklist

The submission should clearly show at least three Kaggle concepts. Prefer five:

- ADK agent or multi-agent workflow
- MCP server tools
- Antigravity usage
- security/privacy features
- deployability/build/run flow
- agent skills

## README sections

Include these sections in the root README:

1. Project overview
2. Problem statement
3. What the builder generates
4. ADK agent architecture
5. MCP tools
6. Generated Android app architecture
7. Privacy and security design
8. How to run the builder
9. How to build the generated app
10. Demo flow
11. Limitations
12. Roadmap
13. Attribution

## Attribution wording

Use careful wording. Do not claim ownership of external learning material.

Recommended text:

```text
We used publicly available PL Coding Android skills as architectural guidance for modular Android development, Jetpack Compose UI, MVI presentation, Koin dependency injection, Room/data-layer structure, navigation, typed error handling, and testing. The PrivateNotes Builder concept, agent workflow, app-generation pipeline, privacy model, generated app template, and capstone implementation were created by our team.
```

If any external code is copied or adapted, include the license and source notice. If the license is unclear, use the material as learning/reference only and do not copy code verbatim.

## Claims to avoid

Do not claim:

- local LLM support in MVP
- OCR support in MVP
- end-to-end encryption
- secure cloud backup
- Play Store readiness
- compliance with GDPR/HIPAA or other legal frameworks

Use accurate MVP language:

```text
The generated MVP app stores entries locally on the device using Room and does not include login or cloud sync.
```

## Demo script

Use this demo scenario:

1. Open Antigravity with the project skills enabled.
2. Enter the app-generation request for FamilyVault.
3. Show extracted app config.
4. Show MCP validation/rendering/build steps.
5. Open the generated Android project.
6. Run the generated app in emulator.
7. Add entries in School and Baby categories.
8. Search for a note.
9. Filter by category.
10. Delete an entry.
11. Open the privacy screen.

## Definition of submission-ready

The skills are submission-ready only when they support producing these artifacts:

- working generated Android app
- README with required concept mapping
- video showing Antigravity and generated app
- attribution and limitations
- no unlicensed copied external code
