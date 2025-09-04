# 📖 Color Hut JSON API Documentation

A lightweight PHP-based JSON API that mimics Firestore-style
**Collections** and **Documents**, stored in JSON files.\
No database required.

------------------------------------------------------------------------

## 🔑 Base URL

    https://api.colorhutbd.xyz/dbv3/index.php

All requests should be made to this base URL.

------------------------------------------------------------------------

## 📂 Collections

### 1. List All Collections

``` http
GET /collections
```

**Response:**

``` json
{
  "collections": ["users", "products", "orders"]
}
```

------------------------------------------------------------------------

### 2. Create a Collection

``` http
POST /collections
```

**Body:**

``` json
{ "name": "users" }
```

**Response:**

``` json
{ "message": "Collection created", "name": "users" }
```

------------------------------------------------------------------------

### 3. Delete a Collection

``` http
DELETE /collections/{collection_name}
```

**Response:**

``` json
{ "message": "Collection deleted" }
```

------------------------------------------------------------------------

## 📑 Documents

### 4. List/Search Documents

``` http
GET /collections/{collection_name}/documents?limit=10&offset=1&search=keyword
```

**Query Parameters:** - `limit` → number of documents per page (default
`10`)\
- `offset` → page number (default `1`)\
- `search` → keyword filter (searches inside document `data`)

**Response:**

``` json
{
  "documents": [
    {
      "id": "doc_1725429943",
      "data": { "title": "Hello World", "status": "active" },
      "created_at": "2025-09-04 12:32:00",
      "updated_at": "2025-09-04 12:32:00"
    }
  ],
  "total": 1,
  "limit": 10,
  "page": 1,
  "total_pages": 1,
  "search": "hello"
}
```

------------------------------------------------------------------------

### 5. Get a Document by ID

``` http
GET /collections/{collection_name}/documents/{document_id}
```

**Response:**

``` json
{
  "id": "doc_1725429943",
  "data": { "title": "Hello World", "status": "active" },
  "created_at": "2025-09-04 12:32:00",
  "updated_at": "2025-09-04 12:32:00"
}
```

------------------------------------------------------------------------

### 6. Create a Document

``` http
POST /collections/{collection_name}/documents
```

**Body (auto-generate ID):**

``` json
{ "data": { "title": "New User", "status": "active" } }
```

**Body (custom ID):**

``` json
{ "id": "user123", "data": { "title": "Custom User", "status": "active" } }
```

**Response:**

``` json
{ "message": "Document created", "id": "user123" }
```

------------------------------------------------------------------------

### 7. Update a Document

``` http
PUT /collections/{collection_name}/documents/{document_id}
```

**Body:**

``` json
{ "data": { "status": "inactive" } }
```

**Response:**

``` json
{ "message": "Document updated", "id": "user123" }
```

------------------------------------------------------------------------

### 8. Delete a Document

``` http
DELETE /collections/{collection_name}/documents/{document_id}
```

**Response:**

``` json
{ "message": "Document deleted", "id": "user123" }
```

------------------------------------------------------------------------

## ⚠️ Notes

-   Data is persisted in JSON files under `/dbv3/collections/`.\
-   `created_at` and `updated_at` timestamps are auto-managed.\
-   Search is **case-insensitive** and scans all fields in `data`.\
-   Pagination uses **page numbers** (not raw offsets).
