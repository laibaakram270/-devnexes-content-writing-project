# Notion Developer API Guide

**Word Count Target**: 1000 words

## 1. Introduction
The Notion API allows developers to read and write data to Notion pages, databases, and blocks programmatically. This guide covers authentication and 3 core endpoints for building integrations.

## 2. Authentication
Notion uses OAuth 2.0 and Internal Integration Tokens.
1. Go to https://www.notion.so/my-integrations
2. Create new integration and copy the "Internal Integration Token"
3. Share databases/pages with your integration

Header format:
`Authorization: Bearer YOUR_INTERNAL_TOKEN`
`Notion-Version: 2022-06-28`

## 3. Base URL
`https://api.notion.com/v1`

## 4. Endpoints

### GET /databases/{database_id}
Retrieve a database.

**cURL:**
```bash
curl -X GET "https://api.notion.com/v1/databases/DATABASE_ID" \
-H "Authorization: Bearer YOUR_TOKEN" \
-H "Notion-Version: 2022-06-28"
**Python:**
```python
import requests
headers = {"Authorization": "Bearer YOUR_TOKEN", "Notion-Version": "2022-06-28"}
response = requests.get("https://api.notion.com/v1/databases/DATABASE_ID", headers=headers)
print(response.json())
**JavaScript:**
```javascript
fetch("https://api.notion.com/v1/databases/DATABASE_ID", {
  headers: {"Authorization": "Bearer YOUR_TOKEN", "Notion-Version": "2022-06-28"}
})
.then(res => res.json())
.then(data => console.log(data));

