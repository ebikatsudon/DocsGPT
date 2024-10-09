# API Endpoints Documentation

*Currently, the application provides the following main API endpoints:*


## 1. `POST` /api/answer 

Retrieves answers to user-provided questions.

**Headers**:

```curl
curl -H "Content-Type: application/json; charset=utf-8"
```

**Sample JSON Request Body**:

```json
{
 "question": "Hi",
 "history": null,
 "api_key": "OPENAI_API_KEY",
 "embeddings_key":  "OPENAI_API_KEY",
 "active_docs": "javascript/.project/ES2015/openai_text-embedding-ada-002/"
}
```

| Key | Data Type | Description | Use |
|-----|-----------|-------------|-----------|
| question | string | The user's question | Required |
| history | string or null | Previous conversation history | Optional |
| api_key | string | Your API key | Required |
| embeddings_key | string | Your embeddings key |  Required |
| active_docs | string | The location of the active documentation | Required |

**Sample Javascript Request**:

```js
// answer (POST http://127.0.0.1:5000/api/answer)
fetch("http://127.0.0.1:5000/api/answer", {
      "method": "POST",
      "headers": {
            "Content-Type": "application/json; charset=utf-8"
      },
      "body": JSON.stringify({"question":"Hi","history":null,"api_key":"OPENAI_API_KEY","embeddings_key":"OPENAI_API_KEY",
      "active_docs": "javascript/.project/ES2015/openai_text-embedding-ada-002/"})
})
.then((res) => res.text())
.then(console.log.bind(console))
```

**Sample JSON Response**:

```json
{
  "answer": "Hi there! How can I help you?\n",
  "query": "Hi",
  "result": "Hi there! How can I help you?\nSOURCES:"
}
```

## 2. `POST` /api/docs_check

Checks if documentation is loaded on the server. Should be run every time the user is switching between libraries (i.e. documentation).

**Headers**:

```curl
curl -H "Content-Type: application/json; charset=utf-8"
```

**Sample JSON Request Body**:

```json
{
 "docs": "javascript/.project/ES2015/openai_text-embedding-ada-002/"
}
```

| Key | Data Type | Description | Use |
|-----|-----------|-------------|-----------|
| docs | string | The location of the documentation | Required |

**Sample Javascript Request**:

```js
// docs_check (POST http://127.0.0.1:5000/api/docs_check)
fetch("http://127.0.0.1:5000/api/docs_check", {
      "method": "POST",
      "headers": {
            "Content-Type": "application/json; charset=utf-8"
      },
      "body": JSON.stringify({"docs":"javascript/.project/ES2015/openai_text-embedding-ada-002/"})
})
.then((res) => res.text())
.then(console.log.bind(console))
```

**Sample JSON Response**:

```json
{
  "status": "exists"
}
```

## `GET` 3. /api/combine

Retrieves information about available vectors and their locations.

**Sample JSON Response:**

Response will include:
* `date`
* `description`
* `docLink`
* `fullName`
* `language`
* `location` (local or docshub)
* `model`
* `name`
* `version`

Example in Docshub and local:

<img width="295" alt="image" src="https://user-images.githubusercontent.com/15183589/224714085-f09f51a4-7a9a-4efb-bd39-798029bb4273.png">

## 4. `POST` /api/upload

Uploads a file for training.

**Request Body**: A multipart/form-data form with file upload and additional fields, including `user` and `name`.

**Sample HTML Request**:

```html
<form action="/api/upload" method="post" enctype="multipart/form-data" class="mt-2">
    <input type="file" name="file" class="py-4" id="file-upload">
    <input type="text" name="user" value="local" hidden>
    <input type="text" name="name" placeholder="Name:">
    
    <button type="submit" class="py-2 px-4 text-white bg-purple-30 rounded-md hover:bg-purple-30 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-purple-30">
        Upload
    </button>
</form>
```

**JSON Response:**

Returns a status and a task ID that can be used to check the task's progress.


## 5. `GET` /api/task_status

Returns the status of a task with `task_id` from `/api/upload`

**Query Parameter**:

| Key | Data Type | Description | Use |
|-----|-----------|-------------|-----------|
| task_id | string | Identifier for an uploaded task | Required |

**Sample JavaScript Fetch Request:**
```js
// Task status (Get http://127.0.0.1:5000/api/task_status)
fetch("http://localhost:5001/api/task_status?task_id=YOUR_TASK_ID", {
      "method": "GET",
      "headers": {
            "Content-Type": "application/json; charset=utf-8"
      },
})
.then((res) => res.text())
.then(console.log.bind(console))
```

**Response:**

There are two types of responses:

1. While the task is still running, the 'current' value will show progress from 0 to 100.
   ```json
   {
     "result": {
       "current": 1
     },
     "status": "PROGRESS"
   }
   ```

2. When task is completed:
   ```json
   {
     "result": {
       "directory": "temp",
       "filename": "install.rst",
       "formats": [
         ".rst",
         ".md",
         ".pdf"
       ],
       "name_job": "somename",
       "user": "local"
     },
     "status": "SUCCESS"
   }
   ```

## 6. `GET` /api/delete_old

Deletes old Vector Stores.

**Query Parameter**:

| Key | Data Type | Description | Use |
|-----|-----------|-------------|-----------|
| task_id | string | Identifier for an uploaded task | Required |

**Sample JavaScript Fetch Request:**
```js
// delete_old (GET http://127.0.0.1:5000/api/delete_old)
fetch("http://localhost:5001/api/delete_old?task_id=YOUR_TASK_ID", {
      "method": "GET",
      "headers": {
            "Content-Type": "application/json; charset=utf-8"
      },
})
.then((res) => res.text())
.then(console.log.bind(console))

```
**Sample JSON Response:**

```json
{ "status": "ok" }
```

### 7. `GET` /api/get_api_keys

Retrieves a list of API keys for the user.

**Sample JavaScript Fetch Request:**
```js
// get_api_keys (GET http://127.0.0.1:5000/api/get_api_keys)
fetch("http://localhost:5001/api/get_api_keys", {
      "method": "GET",
      "headers": {
            "Content-Type": "application/json; charset=utf-8"
      },
})
.then((res) => res.text())
.then(console.log.bind(console))

```
**Sample JSON Response:**

```json
[
      {
        "id": "string",
        "name": "string",
        "key": "string",
        "source": "string"
      },
      ...
    ]
```

### 8. `POST` /api/create_api_key

Creates a new API key for the user.

**Headers**:

```curl
curl -H "Content-Type: application/json; charset=utf-8"
```

**Sample JSON Request Body**:

```json
{
 "name": "Hi",
 "source": null,
 "prompt_id": "OPENAI_API_KEY",
 "chunks":  "OPENAI_API_KEY",
}
```

| Key | Data Type | Description | Use |
|-----|-----------|-------------|-----------|
| name | string | A name for the API key | Required |
| source | string | The source documents to be used | Required |
| prompt_id | string | The prompt ID | Required |
| chunks | string | The number of chunks used to process an answer | Required |

**Sample JavaScript Fetch Request**:

```js
// create_api_key (POST http://127.0.0.1:5000/api/create_api_key)
fetch("http://127.0.0.1:5000/api/create_api_key", {
      "method": "POST",
      "headers": {
            "Content-Type": "application/json; charset=utf-8"
      },
      "body": JSON.stringify({"name":"Example Key Name",
          "source":"Example Source",
          "prompt_id":"creative",
          "chunks":"2"})
})
.then((res) => res.json())
.then(console.log.bind(console))
```

**Sample JSON Response**:

```json
{
  "id": "string",
  "key": "string"
}
```

### 9. `POST` /api/delete_api_key

Deletes a user's API key.

**Headers**:

```curl
curl -H "Content-Type: application/json; charset=utf-8"
```

**Request Body**:

```json
{
 "id": "API_KEY_ID"
}
```

| Key | Data Type | Description | Use |
|-----|-----------|-------------|-----------|
| id | string | The unique identifier of the API key to be deleted | Required |

**Sample JavaScript Fetch Request**:

```js
// delete_api_key (POST http://127.0.0.1:5000/api/delete_api_key)
fetch("http://127.0.0.1:5000/api/delete_api_key", {
      "method": "POST",
      "headers": {
            "Content-Type": "application/json; charset=utf-8"
      },
      "body": JSON.stringify({"id":"API_KEY_ID"})
})
.then((res) => res.json())
.then(console.log.bind(console))
```

**Sample JSON Response:**

```json
{
  "status": "ok"
}
```