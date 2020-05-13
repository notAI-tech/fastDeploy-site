---
layout: default
title: API interface
nav_order: 3
permalink: /api
---

# API interface
{: .no_toc }


This section describes API request and response formats, endpoints supported by fastDeploy. 
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

See **[Best Practices]()** for notes about getting the most out of your hardware.


fastDeploy supports two types of inputs: `JSON` and `FILE`, two API endpoints: `sync` and `async`.

**Input/ Request Type:** 


## Request Type: FILE

  1. FILE input is intended for **predictors with a list of file paths as input**.

  2. This is useful for deploying CV/ Speech Deep Learning models along with the preprocessing needed.

  3. This allows for predictor functions that can only read input from storage.

  4. Input files should be base64 encoded and sent via a POST request in the following format.

**Request Format**
```json
{
  "data": {
    "1.png": "base64 encoded 1.png",
    "2.png": "base64 encoded 2.png"
  }
}
```

**Python example**
```python
import base64
import requests

file_paths = ["1.png", "2.png"]

data = {}

for file_path in file_paths:
    with open(file_path, "rb") as f:
        data[file_path] = base64.b64encode(open(file_path, "rb").read()).decode("utf-8")

# Sync request
response = requests.post("http://IP:PORT/sync", json = {'data': data}).json()

# Async request without webhook
response = requests.post("http://IP:PORT/async", json = {'data': data}).json()
```



## Request Type: JSON

JSON input is intended for inputs that can be sent as json, i.e: Text based models, models with numerical inputs..

**Request format**
```json
{
  "data": [
    some_json_object_1 (string/list/dict ...),
    some_json_object_1 (string/list/dict ...),
  ]
}
```
**Python example**
```python
import requests

data = [INPUT_1, INPUT_2]

# Sync request
response = requests.post("http://IP:PORT/sync", json = {'data': data}).json()

# Async request without webhook
response = requests.post("http://IP:PORT/async", json = {'data': data}).json()
```

## Endpoint: SYNC

`/sync` is the end point for sync inference. i.e: the response of the post request will contain the prediction(s).

**On Success**
- FILE
```json
{
  "prediction": {
    "1.png": ..,
    "2.png": ..
  }, 
  "success": True
}
```

- JSON
```json
{
  "prediction": [
    PRED_1,
    PRED_2
  ], 
  "success": True
}
```

**On Fail**: 
```json
{
  "success": False,
  "reason": REASON
}
```

## Endpoint: ASYNC

`/async` is the endpoint for async inference. i.e: a `unique_id` is returned in response to the request.

The response can be obtained by poling endpoint `/result` or via a webhook (if provided).

**Webhook**
  - Apart from the usual "data" key, async accepts another **optional parameter** `webhook`.
  ```python
  response = requests.post(API_URL, json = {'data': data, 'webhook': WEBHOOK_URL}).json()
  ```
  - If webhook is specified, manager loop calls the webhook with the result and the unique_id.
  - [requestcatcher](https://requestcatcher.com/), [webhook.site](https://webhook.site/) .. provide free, in-browser private webhook listener for testing.
**On success**
```json
{
  "unique_id": "string_unique_id", 
  "success": True
}
```
**On Fail**: 
```json
{
  "success": False,
  "reason": REASON
}
```

## Endpoint: RESULT/ POLING
- Result for a `/async` request can be obtained by poling the endpoint `/result`

**Request format**
```json
{
  "unique_id": "string_unique_id"
}
```

```python
import requests

result = requests.post("http://IP:PORT/result", json={"unique_id": UNIQUE_ID}).json()
status = result['status']
```

Response is same as `/sync`