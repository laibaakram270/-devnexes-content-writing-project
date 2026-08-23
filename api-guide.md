# Notion Developer API Guide

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



### POST /pages
Create a new page in a database.

**cURL:**
```bash
curl -X POST "https://api.notion.com/v1/pages" \
-H "Authorization: Bearer YOUR_TOKEN" \
-H "Notion-Version: 2022-06-28" \
-H "Content-Type: application/json" \
-d '{"parent": {"database_id": "DATABASE_ID"}, "properties": {"Name": {"title": [{"text": {"content": "New Task"}}]}}}'
Python:
pythonimport requests
import json
url = "https://api.notion.com/v1/pages"
headers = {"Authorization": "Bearer YOUR_TOKEN", "Notion-Version": "2022-06-28", "Content-Type": "application/json"}
data = {"parent": {"database_id": "DATABASE_ID"}, "properties": {"Name": {"title": [{"text": {"content": "New Task"}}]}}}
response = requests.post(url, headers=headers, data=json.dumps(data))
print(response.json())
JavaScript:
javascriptfetch("https://api.notion.com/v1/pages", {
  method: "POST",
  headers: {"Authorization": "Bearer YOUR_TOKEN", "Notion-Version": "2022-06-28", "Content-Type": "application/json"},
  body: JSON.stringify({parent: {database_id: "DATABASE_ID"}, properties: {Name: {title: [{text: {content: "New Task"}}]}}})
})
.then(res => res.json())
.then(data => console.log(data));



#### **ENDPOINT 3: PATCH**
```md
### PATCH /pages/{page_id}
Update a page property.

**cURL:**
```bash
curl -X PATCH "https://api.notion.com/v1/pages/PAGE_ID" \
-H "Authorization: Bearer YOUR_TOKEN" \
-H "Notion-Version: 2022-06-28" \
-H "Content-Type: application/json" \
-d '{"properties": {"Status": {"select": {"name": "Done"}}}}'
Python:
import requests
import json
url = "https://api.notion.com/v1/pages/PAGE_ID"
headers = {"Authorization": "Bearer YOUR_TOKEN", "Notion-Version": "2022-06-28", "Content-Type": "application/json"}
data = {"properties": {"Status": {"select": {"name": "Done"}}}}
response = requests.patch(url, headers=headers, data=json.dumps(data))
print(response.json())
JavaScipt:
fetch("https://api.notion.com/v1/pages/PAGE_ID", {
  method: "PATCH",
  headers: {"Authorization": "Bearer YOUR_TOKEN", "Notion-Version": "2022-06-28", "Content-Type": "application/json"},
  body: JSON.stringify({properties: {Status: {select: {name: "Done"}}}})
})
.then(res => res.json())
.then(data => console.log(data));
```
## 4. Error Handling
Notion API returns standard HTTP codes.

| Code | Meaning | Fix |
| --- | --- | --- |
| 401 | Unauthorized | Check your Bearer token |
| 404 | Not Found | Verify database_id or page_id |
| 429 | Rate Limited | Wait 1 second and retry |

Example Python error handling:
```python
try:
    response = requests.post(url, headers=headers, json=data)
    response.raise_for_status()
except requests.exceptions.HTTPError as err:
    print(f"Error: {err}")

