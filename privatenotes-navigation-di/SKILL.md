---
name: privatenotes-navigation-di
description: |
  Navigation and Koin wiring for the generated PrivateNotes app. Use this skill when defining routes, nav graphs, Koin modules, repository injection, ViewModel injection, and Application startup.
---

# PrivateNotes Navigation + Koin

## Navigation routes

Use type-safe routes where supported by the project setup. Otherwise use simple sealed route constants. Prefer simple and buildable over complex.

Recommended route objects:

```kotlin
@Serializable data object EntryListRoute
@Serializable data object AddEntryRoute
@Serializable data class EntryDetailRoute(val entryId: String)
@Serializable data object SettingsPrivacyRoute
```

## App navigation graph

The generated app needs a small graph:

```text
EntryList
├── AddEntry
├── EntryDetail(entryId)
└── SettingsPrivacy
```

## Navigation rules

- Pass IDs, not full objects.
- Load entry details from the ViewModel/repository.
- Keep navigation wiring in one `AppNavHost`.
- Do not make feature packages depend on each other.

## Koin modules

Create simple Koin modules:

```kotlin
val databaseModule = module {
    single {
        Room.databaseBuilder(
            androidContext(),
            PrivateNotesDatabase::class.java,
            "private_notes.db"
        ).build()
    }
    single { get<PrivateNotesDatabase>().knowledgeEntryDao() }
}

val repositoryModule = module {
    single<KnowledgeEntryRepository> {
        RoomKnowledgeEntryRepository(get())
    }
}

val viewModelModule = module {
    viewModel { EntryListViewModel(get(), get()) }
    viewModel { AddEntryViewModel(get(), get()) }
    viewModel { parameters -> EntryDetailViewModel(parameters.get(), get()) }
    viewModel { SettingsPrivacyViewModel(get()) }
}
```

## Application startup

```kotlin
class PrivateNotesApplication : Application() {
    override fun onCreate() {
        super.onCreate()

        startKoin {
            androidContext(this@PrivateNotesApplication)
            modules(
                databaseModule,
                repositoryModule,
                viewModelModule
            )
        }
    }
}
```

Remember to register the application class in `AndroidManifest.xml`.

## Configuration injection

Generated categories should be available from a small config object:

```kotlin
object GeneratedAppConfig {
    const val APP_NAME = "FamilyVault"
    val categories = listOf("School", "Baby", "Housework", "Travel", "Health", "Other")
}
```

Inject a `CategoryProvider` if the app needs testability:

```kotlin
interface CategoryProvider {
    val categories: List<String>
}
```

## Simplicity rule

Do not over-modularize DI. Keep the generated app easy to inspect for the capstone demo.
