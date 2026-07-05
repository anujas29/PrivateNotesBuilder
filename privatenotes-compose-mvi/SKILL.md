---
name: privatenotes-compose-mvi
description: |
  Compose and MVI patterns for the generated PrivateNotes app. Use this skill when creating screens, ViewModels, states, actions, events, UI models, and shared components.
---

# PrivateNotes Compose + MVI

## Core principle

Composables render state and forward actions. Business logic lives in ViewModels, repositories, and domain/use-case code.

## Screen split

For each screen, use:

- `XRoot`: obtains ViewModel, collects state/events, wires navigation callbacks
- `XScreen`: stateless composable that renders state and emits actions

Example:

```kotlin
@Composable
fun EntryListRoot(
    viewModel: EntryListViewModel = koinViewModel(),
    onEntryClick: (String) -> Unit,
    onAddClick: () -> Unit
) {
    val state by viewModel.state.collectAsStateWithLifecycle()

    ObserveAsEvents(viewModel.events) { event ->
        when (event) {
            is EntryListEvent.NavigateToDetail -> onEntryClick(event.entryId)
            EntryListEvent.NavigateToAdd -> onAddClick()
        }
    }

    EntryListScreen(
        state = state,
        onAction = viewModel::onAction
    )
}
```

## State

Use immutable state classes.

```kotlin
data class EntryListState(
    val entries: List<EntryUi> = emptyList(),
    val selectedCategory: String? = null,
    val query: String = "",
    val categories: List<String> = emptyList(),
    val isLoading: Boolean = false
)
```

Annotate with `@Stable` only if needed because lists are present and recomposition warnings appear.

## Actions

Use sealed interfaces.

```kotlin
sealed interface EntryListAction {
    data object OnAddClick : EntryListAction
    data class OnEntryClick(val entryId: String) : EntryListAction
    data class OnQueryChange(val query: String) : EntryListAction
    data class OnCategorySelected(val category: String?) : EntryListAction
    data class OnDeleteClick(val entryId: String) : EntryListAction
}
```

## Events

Use events only for one-time side effects such as navigation and snackbar messages.

```kotlin
sealed interface EntryListEvent {
    data object NavigateToAdd : EntryListEvent
    data class NavigateToDetail(val entryId: String) : EntryListEvent
    data class ShowSnackbar(val message: UiText) : EntryListEvent
}
```

## Required screens

### EntryListScreen

- top app bar with app name
- search field
- category filter chips
- lazy list of entries
- empty state
- floating action button to add entry

### AddEntryScreen

- title field
- body field
- category dropdown/chips
- tags field
- save button
- validation errors

### EntryDetailScreen

- title, body, category, tags, timestamps
- delete button with confirmation
- optional edit button if implemented

### SettingsPrivacyScreen

- local-only explanation
- no cloud sync statement
- delete all data action with confirmation

## Compose rules

- Use `LazyColumn` with stable keys.
- Use `collectAsStateWithLifecycle`.
- Avoid business logic in composables.
- Use `stringResource` for fixed UI text where practical.
- Provide `contentDescription` for meaningful icons.
- Use Material 3 components.
- Keep UI plain and robust; do not over-polish before features work.
