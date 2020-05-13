---
layout: default
title: Free to Use APIs
nav_order: 9
permalink: /free_apis
---

# Description of Free to Use APIs we provide

Signup [**here**](https://tech.notai.tech/signup) for a free API key.

- We don't send any verification emails/ spam or store your email publicly.

- `/sync` is not enabled on the APIs we provide. `/async`, `/result`, webhooks, client-side batching, work as expected.

**Limit**: Maximum number of requests allowed per hour.

**Batch Size**: Maximum client-side batch size allowed per request.

- For example, Limit = 16 and Batch size = 4, allows you to process a maximum of 64 examples per hour.

- `/result` requests are not counted against the LIMIT.
- All `/result` requests are capped at 4 requests per minute.
- We strongly encourage users to use webhooks.  

| Recipe                                                                    | URL                                              | Limit| Batch Size |
|:-------------------------------------------------------------------------:|:------------------------------------------------:|:----:|:----------:|
|[deepsegment_en](https://github.com/bedapudi6788/deepsegment) |https://tech.notai.tech/deepsegment/en/async      |64|16|
|[efficientnet_b2](https://github.com/qubvel/efficientnet)|https://tech.notai.tech/efficientnet/b2/async     |16|4|
|[kaldi_vosk-en_us-aspire](https://github.com/alphacep/vosk-api/blob/master/doc/models.md)|https://tech.notai.tech/efficientnet/b2/async     |16|4|

**Notes**:
- `kaldi_vosk-en_us-aspire` only processes the first 30 seconds of longer audios. i.e: A user is allowed to process `32 minutes` of audio per hour.


The request/response structure is explained [**here.**](https://fastdeploy.notai.tech/api)

Async with webhook example.
```bash
curl -d '{"data": ["text_1", "text_2"], "webhook": "https://fastdeploy.requestcatcher.com"}' -H "Content-Type: application/json" "https://tech.notai.tech/deepsegment/en/async?api_key=API_KEY"
```

```python
import requests

data = {"data": ["text_1", "text_2"], "webhook": "https://fastdeploy.requestcatcher.com"}

requests.post('https://tech.notai.tech/deepsegment/en/async', params={'api_key': API_KEY}, json=data).json()
```
