---
name: privatenotes-room-data-layer
description: |
  Room/local data-layer rules for the generated PrivateNotes app. Use this skill when creating entities, DAOs, repositories, mappers, search queries, category filters, delete actions, or local-only persistence.
---

# PrivateNotes Room Data Layer

## Core principle

The generated app is local-first. All notes are stored in a local Room database. There is no account, no cloud sync, and no network dependency.

## Domain model

```kotlin
data class KnowledgeEntry(
    val id: String,
    val title: String,
    val body: String,
    val category: String,
    val tags: List<String>,
    val createdAt: Long,
    val updatedAt: Long
)
```

## Room entity

```kotlin
@Entity(tableName = "knowledge_entries")
data class KnowledgeEntryEntity(
    @PrimaryKey val id: String,
    val title: String,
    val body: String,
    val category: String,
    val tags: String,
    val createdAt: Long,
    val updatedAt: Long
)
```

Store tags as a comma-separated or JSON string for MVP simplicity. Use a mapper to convert between entity and domain model.

## DAO requirements

The DAO should provide:

```kotlin
@Query("SELECT * FROM knowledge_entries ORDER BY updatedAt DESC")
fun observeEntries(): Flow<List<KnowledgeEntryEntity>>

@Query("SELECT * FROM knowledge_entries WHERE id = :id")
suspend fun getEntryById(id: String): KnowledgeEntryEntity?

@Query(
    """
    SELECT * FROM knowledge_entries
    WHERE title LIKE '%' || :query || '%'
       OR body LIKE '%' || :query || '%'
       OR tags LIKE '%' || :query || '%'
    ORDER BY updatedAt DESC
    """
)
fun searchEntries(query: String): Flow<List<KnowledgeEntryEntity>>

@Query("SELECT * FROM knowledge_entries WHERE category = :category ORDER BY updatedAt DESC")
fun observeEntriesByCategory(category: String): Flow<List<KnowledgeEntryEntity>>

@Upsert
suspend fun upsertEntry(entry: KnowledgeEntryEntity)

@Query("DELETE FROM knowledge_entries WHERE id = :id")
suspend fun deleteEntry(id: String)

@Query("DELETE FROM knowledge_entries")
suspend fun deleteAllEntries()
```

## Repository interface

```kotlin
interface KnowledgeEntryRepository {
    fun observeEntries(): Flow<List<KnowledgeEntry>>
    fun searchEntries(query: String): Flow<List<KnowledgeEntry>>
    fun observeEntriesByCategory(category: String): Flow<List<KnowledgeEntry>>
    suspend fun getEntryById(id: String): Result<KnowledgeEntry, EntryDataError>
    suspend fun saveEntry(entry: KnowledgeEntry): EmptyResult<EntryDataError>
    suspend fun deleteEntry(id: String): EmptyResult<EntryDataError>
    suspend fun deleteAllEntries(): EmptyResult<EntryDataError>
}
```

## Error handling

Expected failures must return typed errors, not raw exceptions.

Use feature-specific errors:

```kotlin
enum class EntryDataError : Error {
    NOT_FOUND,
    DISK_FULL,
    INVALID_INPUT,
    UNKNOWN
}
```

## Search behavior

- Empty query returns recent entries.
- Search should match title, body, and tags.
- Category filtering can be combined with search if requested.
- Keep search simple for MVP; no full-text search unless explicitly requested.

## Privacy rules

- Never add remote data sources in MVP.
- Do not log note body content.
- Do not include sample private data in production templates.
- Delete means remove from local Room database.
