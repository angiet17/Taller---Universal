# Taller---Universal

## 📌 Project Overview

This project was developed as part of a practical NoSQL workshop at **Universal Studios Colombia**. The goal was to design and build a **Data Lake** for an online record store using **MongoDB** as the database engine.

The database models albums as collections and songs as documents, covering six international and Latin American artists from different musical genres. The project was structured in three progressive tasks: initial database creation, data updates, and record deletion.

---

## 🗄️ Database Structure

- **Database name:** `universal_studios_colombia`
- **Each album** → one MongoDB collection
- **Each song** → one document inside its collection

### Collections

| Collection | Artist | Album | Year |
|---|---|---|---|
| `lady_gaga_a_star_is_born` | Lady Gaga | A Star Is Born Soundtrack | 2018 |
| `diomedes_diaz_brindo_con_el_alma` | Diomedes Díaz | Brindo Con El Alma | 1986 |
| `michael_jackson_thriller` | Michael Jackson | Thriller | 1982 |
| `queen_a_night_at_the_opera` | Queen | A Night at the Opera | 1975 |
| `ivy_queen_diva` | Ivy Queen | Diva | 2003 |

> ⚠️ The BTS collection (`bts_proof`) was created in Tasks 1 and 2, then fully dropped in Task 3.

---

## 📋 Data Model

Each document (song) follows this structure:

```json
{
  "_id": "lgasib_001",
  "titulo": "Black Eyes",
  "anio_salida": 2018,
  "autor": "Lady Gaga",
  "id_imagen_portada": "lady_gaga_a_star_is_born.jpg",
  "genero": "Pop/Drama",
  "numero_pista": 1
}
```

### Field Reference

| Field | Type | Description |
|---|---|---|
| `_id` | String | Unique document identifier |
| `titulo` | String | Song title |
| `anio_salida` | Number | Release year |
| `autor` | String | Artist or band name |
| `id_imagen_portada` | String | Album cover image filename |
| `genero` | String | Musical genre *(optional)* |
| `numero_pista` | Number | Track number *(optional)* |

---

## 🌿 Branch Structure

```
📁 Repository
├── 🌿 main              → Task 1: Initial database (3 songs per artist)
├── 🌿 actualizaciones   → Task 2: Updated database (5 songs per artist)
└── 🌿 eliminaciones     → Task 3: Final database (3 songs per artist, BTS removed)
```

---

## ✅ Task 1 — Initial Database (branch: `main`)

### Description
Created the MongoDB database with one album per artist, inserting the most well-known songs from each album.

### Songs inserted per artist

**Lady Gaga — A Star Is Born Soundtrack**
- Black Eyes
- Somewhere Over The Rainbow - Dialogue
- La Vie En Rose

**Diomedes Díaz — Brindo Con El Alma**
- Sin Medir Distancias
- Ayúdame A Quererte
- Brindo Con El Alma

**BTS — Proof**
- No More Dream
- Born Singer
- I NEED U

**Michael Jackson — Thriller**
- Billie Jean
- Thriller
- Beat It

**Queen — A Night at the Opera**
- Love Of My Life
- Bohemian Rhapsody
- Death On Two Legs (Dedicated To...)

**Ivy Queen — Diva**
- Yo Quiero Bailar
- Tuya Soy
- Venganza

### Deliverables
- `images/` folder with album covers
- CSV export of the full database
- BSON files for each collection and document

---

## 🔄 Task 2 — Database Update (branch: `actualizaciones`)

### Description
Each album was expanded with two lesser-known songs from the same album, increasing each collection from 3 to 5 documents.

### Songs added per artist

| Artist | Songs Added |
|---|---|
| Lady Gaga | Before I Cry, Why Did You Do That? |
| Diomedes Díaz | Los Sabanales, Pasajeros De La Vida |
| BTS | Quotation Mark, Jump (Demo Ver.) |
| Michael Jackson | Baby Be Mine, The Lady in My Life |
| Queen | '39, Good Company |
| Ivy Queen | En El Principio, Somos Raperos Pero No Delincuentes |

### Deliverables
- Updated CSV exports for all collections
- Updated BSON files
- Corrected `anio_salida` for Diomedes Díaz (1986, not 1992)

---

## 🗑️ Task 3 — Record Deletion (branch: `eliminaciones`)

### Description
Deletion operations were performed on the database: two songs were removed from each album, and the BTS collection was fully dropped.

### Documents deleted per artist

| Artist | Songs Removed |
|---|---|
| Lady Gaga | Before I Cry, Why Did You Do That? |
| Diomedes Díaz | Los Sabanales, Pasajeros De La Vida |
| Michael Jackson | Baby Be Mine, The Lady in My Life |
| Queen | '39, Good Company |
| Ivy Queen | En El Principio, Somos Raperos Pero No Delincuentes |

### Collection dropped
- `bts_proof` — fully removed from the database

### Deliverables
- CSV exports after deletions
- BSON files of remaining collections
- `images/` folder updated (removed `bts_proof.jpg`)

---

## 🎨 Design Decisions

- **_id format:** Custom string IDs (e.g. `lgasib_001`) were used instead of MongoDB's default ObjectId to make documents more readable and traceable.
- **Album-as-collection model:** Each album was modeled as a separate collection rather than grouping all songs in one collection, following the workshop's required structure.
- **Optional fields:** Extra fields like `genero` and `numero_pista` were added to enrich the documents beyond the minimum required.
- **Cover images:** Each collection references a single album cover image shared across all its documents via the `id_imagen_portada` field.

---

## 💡 Findings & Learnings

- MongoDB's document model is highly flexible — adding optional fields to some documents without affecting others required no schema changes.
- Verifying tracklist accuracy before inserting data is critical. During this workshop, the release year for *Brindo Con El Alma* (Diomedes Díaz) had to be corrected from 1992 to **1986** after cross-checking official sources.
- The `mongodump` command is essential for generating BSON exports, as MongoDB Compass only supports CSV export natively.
- Working with multiple branches in Git helped keep each task isolated and made it easy to review the evolution of the database across tasks.
- Dropping a collection in MongoDB is irreversible — always verify the target before confirming the operation.

---

## 🚀 How to Replicate This Project

### Prerequisites
- MongoDB installed and running on `localhost:27017`
- MongoDB Compass (GUI) or `mongosh` (terminal)
- `mongodump` / `mongorestore` tools installed

### Import the database from BSON

```bash
mongorestore --db universal_studios_colombia ./taller_nosql_backup/universal_studios_colombia/
```

### Import a specific collection

```bash
mongorestore --db universal_studios_colombia \
  --collection lady_gaga_a_star_is_born \
  ./taller_nosql_backup/universal_studios_colombia/lady_gaga_a_star_is_born.bson
```

### Verify the import in mongosh

```js
use universal_studios_colombia
show collections
db.lady_gaga_a_star_is_born.find().pretty()
```

---

## 👥 Team

Developed by a group of 3 students as part of the NoSQL Databases practical workshop at Universal Studios Colombia.

---

*Workshop — NoSQL Databases with MongoDB | Universal Studios Colombia*
