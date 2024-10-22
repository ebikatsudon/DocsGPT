# API Endpoints Documentation

The base URL for all API paths is `http://localhost.7901/`.

Currently, the application provides the following endpoints:


## 1. `POST` /api/answer 

Responds with answers to user-provided questions.

**Headers**:

```curl
curl -H "Content-Type: application/json; charset=utf-8"
```

**Sample JSON Request Body**:

```json
{
 "question": "Summarize current context",
 "api_key": "OPENAI_API_KEY",
 "embeddings_key":  "OPENAI_API_KEY",
 "active_docs": "67088ee3d14d6f75727f218c"
}
```

| Key | Data Type | Description | Use |
|-----|-----------|-------------|-----------|
| question | string | The user's question. | Required |
| api_key | string | Your API key. | Optional |
| embeddings_key | string | Your embeddings key. | Optional |
| active_docs | string | The ID of the active documentation. | Required |

**Sample Javascript Fetch Request**:

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

```js
const myHeaders = new Headers();
myHeaders.append("Content-Type", "application/json; charset=utf-8");

const raw = "{\r\n \"question\": \"Hi\",\r\n \"active_docs\": \"670d9cc211b0b55a9b68d9c3\"\r\n}";

const requestOptions = {
  method: "POST",
  headers: myHeaders,
  body: raw,
  redirect: "follow"
};

fetch("http://localhost:7091/api/answer", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.error(error));
  ```

**Sample JSON Response**:

```json
{
  "answer": "Hi there! How can I help you?\n",
  "query": "Hi",
  "result": "Hi there! How can I help you?\nSOURCES:"
}
```

```json
{
    "answer": "Hello! How can I assist you today? If you have any questions or need help with something specific, feel free to ask!",
    "conversation_id": "670f352a2ad68e881af52589",
    "sources": [
        {
            "source": "https://docs.docsgpt.cloud/API/API-docs",
            "text": "API Endpoints Documentation - DocsGPT DocumentationWelcome to the new DocsGPT ü¶ñ docs! üëãDocsGPT DocsGitHubGitHub (opens in a new tab)DiscordDiscord (opens in a new tab)HomeAPIüóÇÔ∏èÔ∏è API-docsüîê API Keys guideDeploying‚òÅÔ∏è Hosting DocsGPT‚ö°Ô∏èQuickstartüöÇDeploying on Railway‚ò∏Ô∏èDeploying on KubernetesExtensionsüí¨Ô∏è Chatwoot ExtensionüèóÔ∏è Widget setupüåê Chrome ExtensionGuidesÔ∏èüíª Customising Promptsüì• Training on docsÔ∏èü§ñ How to use different LLM'süí≠Ô∏è Avoiding hallucinationsLightOn This Page1. /api/answer2. /api/docs_check3. /api/combine4. /api/upload5. /api/task_status6. /api/delete_old7. /api/get_api_keys8. /api/create_api_key9. /api/delete_api_keyQuestion? Give us feedback ‚Üí (opens in a new tab)Edit this pageAPIüóÇÔ∏èÔ∏è API-docsAPI Endpoints Documentation\nCurrently, the application provides the following main API endpoints:\n1. /api/answer\nDescription:\nThis endpoint is used to request answers to user-provided questions.\nRequest:\nMethod: POST\nHeaders: Content-Type should be set to application/json; charset=utf-8\nRequest Body: JSON object with the following fields:\n\nquestion ‚Äî The user's question.\nhistory  ‚Äî  (Optional) Previous conversation history.\napi_key‚Äî Your API key.\nembeddings_key  ‚Äî  Your embeddings key.\nactive_docs ‚Äî The location of active documentation.\n\nHere is a JavaScript Fetch Request example:\n// answer (POST http://127.0.0.1:5000/api/answer)\nfetch(\"http://127.0.0.1:5000/api/answer\", {\n      \"method\": \"POST\",\n      \"headers\": {\n            \"Content-Type\": \"application/json; charset=utf-8\"\n      },\n      \"body\": JSON.stringify({\"question\":\"Hi\",\"history\":null,\"api_key\":\"OPENAI_API_KEY\",\"embeddings_key\":\"OPENAI_API_KEY\",\n      \"active_docs\": \"javascript/.project/ES2015/openai_text-embedding-ada-002/\"})\n})\n.then((res) => res.text())\n.then(console.log.bind(console))\nResponse\nIn response, you will get a JSON document containing the answer, query and result:\n{\n  \"answer\": \"Hi there! How can I help you?\\n\",\n  \"query\": \"Hi\",\n  \"result\": \"Hi there! How can I help you?\\nSOURCES:\"\n}\n2. /api/docs_check\nDescription:\nThis endpoint will make sure documentation is loaded on the server (just run it every time user is switching between libraries (documentations)).\nRequest:\nMethod: POST\nHeaders: Content-Type should be set to application/json; charset=utf-8\nRequest Body: JSON object with the field:\n\ndocs ‚Äî The location of the documentation:\n\n// docs_check (POST http://127.0.0.1:5000/api/docs_check)\nfetch(\"http://127.0.0.1:5000/api/docs_check\", {\n      \"method\": \"POST\",\n      \"headers\": {\n            \"Content-Type\": \"application/json; charset=utf-8\"\n      },\n      \"body\": JSON.stringify({\"docs\":\"javascript/.project/ES2015/openai_text-embedding-ada-002/\"})\n})\n.then((res) => res.text())\n.then(console.log.bind(console))\nResponse:\nIn response, you will get a JSON document like this one indicating whether the documentation exists or not:\n{\n  \"status\": \"exists\"\n}\n3. /api/combine\nDescription:\nThis endpoint provides information about available vectors and their locations with a simple GET request.\nRequest:\nMethod: GET\nResponse:\nResponse will include:\n\ndate\ndescription\ndocLink\nfullName\nlanguage\nlocation (local or docshub)\nmodel\nname\nversion\n\nExample of JSON in Docshub and local:\n\n4. /api/upload\nDescription:\nThis endpoint is used to upload a file that needs to be trained, response is JSON with task ID, which can be used to check on task's progress.\nRequest:\nMethod: POST\nRequest Body: A multipart/form-data form with file upload and additional fields, including user and name.\nHTML example:\n<form action=\"/api/upload\" method=\"post\" enctype=\"multipart/form-data\" class=\"mt-2\">\n    <input type=\"file\" name=\"file\" class=\"py-4\" id=\"file-upload\">\n    <input type=\"text\" name=\"user\" value=\"local\" hidden>\n    <input type=\"text\" name=\"name\" placeholder=\"Name:\">\n    \n    <button type=\"submit\" class=\"py-2 px-4 text-white bg-purple-30 rounded-md hover:bg-purple-30 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-purple-30\">\n        Upload\n    </button>\n</form>\nResponse:\nJSON response with a status and a task ID that can be used to check the task's progress.\n5. /api/task_status\nDescription:\nThis endpoint is used to get the status of a task (task_id) from /api/upload\nRequest:\nMethod: GET\nQuery Parameter: task_id (task ID to check)\nSample JavaScript Fetch Request:\n// Task status (Get http://127.0.0.1:5000/api/task_status)\nfetch(\"http://localhost:5001/api/task_status?task_id=YOUR_TASK_ID\", {\n      \"method\": \"GET\",\n      \"headers\": {\n            \"Content-Type\": \"application/json; charset=utf-8\"\n      },\n})\n.then((res) => res.text())\n.then(console.log.bind(console))\nResponse:\nThere are two types of responses:\n\n\nWhile the task is still running, the 'current' value will show progress from 0 to 100.\n{\n  \"result\": {\n    \"current\": 1\n  },\n  \"status\": \"PROGRESS\"\n}\n\n\nWhen task is completed:\n{\n  \"result\": {\n    \"directory\": \"temp\",\n    \"filename\": \"install.rst\",\n    \"formats\": [\n      \".rst\",\n      \".md\",\n      \".pdf\"\n    ],\n    \"name_job\": \"somename\",\n    \"user\": \"local\"\n  },\n  \"status\": \"SUCCESS\"\n}\n\n\n6. /api/delete_old\nDescription:\nThis endpoint is used to delete old Vector Stores.\nRequest:\nMethod: GET\nQuery Parameter: task_id\nSample JavaScript Fetch Request:\n// delete_old (GET http://127.0.0.1:5000/api/delete_old)\nfetch(\"http://localhost:5001/api/delete_old?task_id=YOUR_TASK_ID\", {\n      \"method\": \"GET\",\n      \"headers\": {\n            \"Content-Type\": \"application/json; charset=utf-8\"\n      },\n})\n.then((res) => res.text())\n.then(console.log.bind(console))\n \nResponse:\nJSON response indicating the status of the operation:\n{ \"status\": \"ok\" }\n7. /api/get_api_keys\nDescription:\nThe endpoint retrieves a list of API keys for the user.\nRequest:\nMethod: GET\nSample JavaScript Fetch Request:\n// get_api_keys (GET http://127.0.0.1:5000/api/get_api_keys)\nfetch(\"http://localhost:5001/api/get_api_keys\", {\n      \"method\": \"GET\",\n      \"headers\": {\n            \"Content-Type\": \"application/json; charset=utf-8\"\n      },\n})\n.then((res) => res.text())\n.then(console.log.bind(console))\n \nResponse:\nJSON response with a list of created API keys:\n[\n      {\n        \"id\": \"string\",\n        \"name\": \"string\",\n        \"key\": \"string\",\n        \"source\": \"string\"\n      },\n      ...\n    ]\n8. /api/create_api_key\nDescription:\nCreate a new API key for the user.\nRequest:\nMethod: POST\nHeaders: Content-Type should be set to application/json; charset=utf-8\nRequest Body: JSON object with the following fields:\n\nname ‚Äî A name for the API key.\nsource ‚Äî The source documents that will be used.\nprompt_id ‚Äî The prompt ID.\nchunks ‚Äî The number of chunks used to process an answer.\n\nHere is a JavaScript Fetch Request example:\n// create_api_key (POST http://127.0.0.1:5000/api/create_api_key)\nfetch(\"http://127.0.0.1:5000/api/create_api_key\", {\n      \"method\": \"POST\",\n      \"headers\": {\n            \"Content-Type\": \"application/json; charset=utf-8\"\n      },\n      \"body\": JSON.stringify({\"name\":\"Example Key Name\",\n          \"source\":\"Example Source\",\n          \"prompt_id\":\"creative\",\n          \"chunks\":\"2\"})\n})\n.then((res) => res.json())\n.then(console.log.bind(console))\nResponse\nIn response, you will get a JSON document containing the id and key:\n{\n  \"id\": \"string\",\n  \"key\": \"string\"\n}\n9. /api/delete_api_key\nDescription:\nDelete an API key for the user.\nRequest:\nMethod: POST\nHeaders: Content-Type should be set to application/json; charset=utf-8\nRequest Body: JSON object with the field:\n\nid ‚Äî The unique identifier of the API key to be deleted.\n\nHere is a JavaScript Fetch Request example:\n// delete_api_key (POST http://127.0.0.1:5000/api/delete_api_key)\nfetch(\"http://127.0.0.1:5000/api/delete_api_key\", {\n      \"method\": \"POST\",\n      \"headers\": {\n            \"Content-Type\": \"application/json; charset=utf-8\"\n      },\n      \"body\": JSON.stringify({\"id\":\"API_KEY_ID\"})\n})\n.then((res) => res.json())\n.then(console.log.bind(console))\nResponse:\nIn response, you will get a JSON document indicating the status of the operation:\n{\n  \"status\": \"ok\"\n}Homeüîê API Keys guideLightMIT 2024 ¬© DocsGPT",
            "title": "API Endpoints Documentation - DocsGPT Documentation"
        }
    ]
}
```

## 2. `POST` /api/docs_check

Checks if documentation is loaded on the server. Should be run every time the user is switching between documentation sources.

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
| docs | string | The location of the documentation. | Required |

**Sample Javascript Request**:

```js
const myHeaders = new Headers();
myHeaders.append("Content-Type", "application/json");

const raw = JSON.stringify({
  "docs": "default"
});

const requestOptions = {
  method: "POST",
  headers: myHeaders,
  body: raw,
  redirect: "follow"
};

fetch("http://localhost:7091/api/docs_check", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.error(error));
```

**Sample JSON Response**:

```json
{
  "status": "exists"
}
```

## `GET` 3. /api/combine

Retrieves information about available vectors.

**Sample JSON Response:**

```json
[
  {
    "date": "default",
    "location": "remote",
    "model": "huggingface_sentence-transformers/all-mpnet-base-v2",
    "name": "default",
    "retriever": "classic",
    "tokens": ""
  },
  {
    "date": "Wed, 31 Jan 2024 12:00:00 GMT",
    "id": "670daed611b0b55a9b68d9c6",
    "location": "local",
    "model": "huggingface_sentence-transformers/all-mpnet-base-v2",
    "name": "Webpage Documentation",
    "retriever": "classic",
    "syncFrequency": "daily",
    "tokens": "2881"
  },
  {
    "date": "Wed, 31 Jan 2024 12:00:00 GMT",
    "id": "67088ee3d14d6f75727f218c",
    "location": "local",
    "model": "huggingface_sentence-transformers/all-mpnet-base-v2",
    "name": "API-docs.md",
    "retriever": "classic",
    "syncFrequency": null,
    "tokens": "2030"
  },
  {
    "date": "duckduck_search",
    "location": "custom",
    "model": "huggingface_sentence-transformers/all-mpnet-base-v2",
    "name": "DuckDuckGo Search",
    "retriever": "duckduck_search",
    "tokens": ""
  }
]
```

| Key | Data Type | Description | Use |
|-----|-----------|-------------|-----------|
| date | string | When the document was uploaded. | Required |
| id | string | ID of the uploaded document. | Optional |
| location | string | Where the document is stored. | Required |
| model | string | The LLM model used for training the document. |  Required |
| name | string | The name of the document. | Required |
| retriever | string | The retriever used to return the document. | Required |
| syncFrequency | string | How often remote documentation is synced with the origin. Can be never, daily, weekly, monthly, or null. | Optional |
| tokens | string | Number of token uses for the document. | Required |

The JSON response values can also be viewed on [DocsHUB](https://github.com/arc53/DocsHUB), if the documentation is stored there.

<img width="295" alt="image" src="https://user-images.githubusercontent.com/15183589/224714085-f09f51a4-7a9a-4efb-bd39-798029bb4273.png">

On DocsHub, additional metadata fields include:

| Key | Data Type | Description | Use |
|-----|-----------|-------------|-----------|
| description | string | A description of the document's contents. | Required |
| docLink | string | The path to the document. | Optional |
| fullName | string | The document's full name. | Required |
| language | string | The LLM model used for training the document. |  Required |
| version | string | The document version | Optional |

## 4. `POST` /api/upload

Uploads a document for training.

**Request Body**: A multipart/form-data object with the following fields:

* `file`: The file to be uploaded from local device
* `user`: The source of the upload
* `name`: The user-designated file name

**Sample JavaScript Fetch Request**:

```js
const formdata = new FormData();
formdata.append("file", fileInput.files[0], "LOCAL-FILE-PATH");
formdata.append("user", "local");
formdata.append("name", "Name");

const requestOptions = {
  method: "POST",
  body: formdata,
  redirect: "follow"
};

fetch("http://localhost:7091/api/upload", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.error(error));
```

**JSON Response:**

Returns a status and a task ID that can be used to check the task's progress.

```json
{
  "success": true,
  "task_id": "cef0a8f8-22a3-452f-bf7b-29d181c83ad9"
}
```

## 5. `GET` /api/task_status

Returns the status of a file upload with designated `task_id` from `/api/upload`.

**Query Parameter**:

| Key | Data Type | Description | Use |
|-----|-----------|-------------|-----------|
| task_id | string | Identifier for a task | Required |

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

1. While the task is running (the `current` value shows progress from 0 to 100):

   ```json
   {
     "result": {
       "current": 1
     },
     "status": "PROGRESS"
   }
   ```

2. When the task is completed:

   ```json
   {
     "result": {
       "directory": "inputs",
       "filename": "API-docs.md",
       "formats": [
         ".rst",
         ".md",
         ".pdf"
         ".txt"
         ".docx"
         ".csv"
         ".epub"
         ".html"
         ".mdx"
       ],
       "name_job": "API-docs",
       "user": "local"
     },
     "status": "SUCCESS"
   }
   ```

**Error Messages**

```json
// If task_id is not provided, returns an error
{
    "message": "Task ID is required",
    "success": false
}
```

## 6. `GET` /api/delete_old

Deletes old vector stores.

**Query Parameter**:

| Key | Data Type | Description | Use |
|-----|-----------|-------------|-----------|
| source_id | string | The ID of the document to be deleted | Required |

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
{
    "success": true
}
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
    "chunks": "2",
    "id": "670f41429e396d5266b1fea8",
    "key": "1f42...2f3e",
    "name": "API-docs",
    "prompt_id": "default",
    "source": "API-docs"
  },
  {
    "chunks": "2",
    "id": "670f424d2ad68e881af5258b",
    "key": "009f...34c3",
    "name": "DuckDuckGo Search",
    "prompt_id": "default",
    "source": "default"
  }
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
  "name":"API-docs",
  "prompt_id":"default",
  "chunks":"2",
  "source":"670d9cc211b0b55a9b68d9c3"
}
```

| Key | Data Type | Description | Use |
|-----|-----------|-------------|-----------|
| name | string | A name for the API key. | Required |
| source | string | The source documents to be used. | Required |
| prompt_id | string | The prompt ID. | Required |
| chunks | string | The number of chunks used to process an answer. | Required |

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

```js
const myHeaders = new Headers();
myHeaders.append("Content-Type", "application/json");

const raw = JSON.stringify({
  "name": "API-docs",
  "prompt_id": "default",
  "chunks": "2",
  "source": "670d9cc211b0b55a9b68d9c3"
});

const requestOptions = {
  method: "POST",
  headers: myHeaders,
  body: raw,
  redirect: "follow"
};

fetch("http://localhost:7091/api/create_api_key", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.error(error));
```

**Sample JSON Response**:

```json
{
  "id": "670f46162ad68e881af5258e",
  "key": "da6c078a-fa07-48a9-9ea1-a5e610d9379b"
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
  "success": true
}
```

## 10. `GET` /api/get_conversations

Returns all recorded conversations.

**Sample JSON Response**

## 11. `POST` /stream
