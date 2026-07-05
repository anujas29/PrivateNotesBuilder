# PrivateNotesBuilder

# Privacy-Focused Android App Builder Agent Skills

Welcome to this collection of custom AI Agent Skills! This repository contains a suite of specialized skills designed to empower AI coding agents to build complete, local-first, privacy-focused Android notes or journaling applications from scratch.

By providing these skills to your AI assistant, it gains the context and architectural knowledge required to build modern, robust, and beautiful Android apps mimicking production-level apps (like Google Keep or Pixel Journal) — without relying on cloud storage or external trackers.

## 🌟 Features

This repository enables an agent to generate apps with the following modern Android tech stack and features:
- **Local-First Architecture:** Ensures absolute user privacy by relying completely on local on-device persistence. No cloud, no trackers.
- **Jetpack Compose:** Uses modern declarative UI to build gorgeous, responsive, and dynamic user interfaces.
- **MVI Architecture (Model-View-Intent):** Ensures predictable, scalable, and stable state management in the UI.
- **Room Database:** Powerful and structured SQLite abstraction for the data layer.
- **Koin for Dependency Injection:** Lightweight and flexible DI specifically suited for Kotlin and Android.
- **Customizable UI Themes:** Dynamic color palettes, material design components, dark mode, and masonry grid layouts.

## 🛠 Included Agent Skills

This repository includes the following specialized skills, each acting as a module of knowledge for the AI agent:

- **`privatenotes-project-context`**: Defines the overarching goal and scope of the privacy-focused app.
- **`privatenotes-privacy-security`**: Enforces strict local-only storage architectures and security guidelines to maintain user privacy.
- **`privatenotes-android-template-architecture`**: Teaches the agent the clean architecture structure spanning Data, Domain, and Presentation layers.
- **`privatenotes-room-data-layer`**: Provides templates and patterns for building robust Room databases, Entities, and DAOs.
- **`privatenotes-compose-mvi`**: Guides the agent on implementing the MVI pattern using Kotlin Flows, StateFlow, and Jetpack Compose.
- **`privatenotes-navigation-di`**: Instructions on setting up Navigation Compose and Koin for seamless routing and dependency injection.
- **`privatenotes-testing-demo`**: Contains scripts and instructions for validating and testing the generated codebase.
- **`privatenotes-adk-agent-workflow`**: Provides a step-by-step workflow for the agent to follow during the app generation process.
- **`privatenotes-submission-readiness`**: Rules for finalizing, polishing, and verifying the application for production or deployment.

## 🚀 How to Use

1. **Clone the Repository:** Clone this repository into your local workspace.
2. **Load Customizations:** Direct your AI coding assistant (such as Antigravity/Gemini) to the workspace so it can automatically detect and load these skills.
3. **Prompt the Agent:** Ask the agent to generate your custom application. You can be specific about your desired theme!
   
   *Example prompts:*
   > "Generate a local-first note-taking app that looks like Google Keep."
   
   > "Build a new Android app called 'PvtJournal'. I want to be able to write text, add a color palette for the background, use tags, and store everything locally using a Pixel Journal UI style."

4. **Review & Run:** Watch as the agent systematically scaffolds the project, builds the Room database, sets up Dependency Injection, creates the MVI UI, and prepares the app. Once finished, compile and run it on your emulator or physical Android device!

## 🔒 Privacy First

We believe that journals and notes are personal. By leveraging these skills, the AI agent is instructed never to include SDKs, network sync libraries, or trackers that could compromise your user data. What happens on your device, stays on your device.

---
*Happy building and journalling!*
