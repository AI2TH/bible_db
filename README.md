# Global Bible Databases (Standalone SQLite with FTS5)

High-performance, standalone SQLite databases for world Bible translations.
Each Bible translation has its own individual .db file containing complete canonical verses and a built-in **FTS5 (Full-Text Search 5)** virtual table.

## Database Schema

Each database contains:

\\sql
-- Metadata table
CREATE TABLE metadata (
    key TEXT PRIMARY KEY,
    value TEXT
);

-- Canonical books
CREATE TABLE books (
    book_number INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    abbreviation TEXT NOT NULL,
    testament TEXT NOT NULL CHECK(testament IN ('OT', 'NT')),
    total_chapters INTEGER NOT NULL
);

-- Verses table
CREATE TABLE verses (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    book_number INTEGER NOT NULL,
    chapter INTEGER NOT NULL,
    verse_number INTEGER NOT NULL,
    text TEXT NOT NULL,
    UNIQUE(book_number, chapter, verse_number)
);

-- FTS5 full-text search index
CREATE VIRTUAL TABLE verses_fts USING fts5(
    text,
    content=verses,
    content_rowid=id,
    tokenize='unicode61'
);
\
## Direct Download URL Pattern

You can pull any Bible database directly using raw GitHub URLs:
\https://raw.githubusercontent.com/AI2TH/bible_db/main/<VERSION_NAME>.db
Example:
\https://raw.githubusercontent.com/AI2TH/bible_db/main/KJV.db\https://raw.githubusercontent.com/AI2TH/bible_db/main/ChiUn.db\https://raw.githubusercontent.com/AI2TH/bible_db/main/FreBBB.db\https://raw.githubusercontent.com/AI2TH/bible_db/main/GerBoLut.db\https://raw.githubusercontent.com/AI2TH/bible_db/main/SpaRV.dbEOF
