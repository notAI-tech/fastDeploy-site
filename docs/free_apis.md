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

**URL: https://tech.notai.tech**

| Recipe                                                                    | Endpoint                                      | Limit| Batch Size | Input Type |
|:-------------------------------------------------------------------------:|:------------------------------------------------:|:----:|:----------:|:----------:|
|[deepsegment_en](https://github.com/bedapudi6788/deepsegment) |/deepsegment/en/async      |64|16| [JSON](https://fastdeploy.notai.tech/api#request-type-json) |
|[efficientnet_b2](https://github.com/qubvel/efficientnet)|/efficientnet/b2/async     |16|4| [FILE](https://fastdeploy.notai.tech/api#request-type-file) |
|[kaldi_vosk-en_us-aspire](https://github.com/alphacep/vosk-api/blob/master/doc/models.md)|/kaldi/vosk_aspire/async     |16|4| [FILE](https://fastdeploy.notai.tech/api#request-type-file) |
|[audio_classification_yamnet](https://github.com/tensorflow/models/blob/master/research/audioset/yamnet/)|/audio_classification/yamnet/async|32|8| [FILE](https://fastdeploy.notai.tech/api#request-type-file) |
|[craft_text_detection](https://github.com/faustomorales/keras-ocr/)|/text_detection/async	     |32|4| [FILE](https://fastdeploy.notai.tech/api#request-type-file) |
|[nudeclassifier](https://github.com/bedapudi6788/NudeNet)|/nudeclassifier/async		     |32|4| [FILE](https://fastdeploy.notai.tech/api#request-type-file) |
|[transformer_sentiment](https://github.com/huggingface/transformers)|/transformer/sentiment/async	     |32|8| [JSON](https://fastdeploy.notai.tech/api#request-type-json) |



**Notes**:
- `kaldi_vosk-en_us-aspire` only processes the first 30 seconds of longer audios. i.e: A user is allowed to process `32 minutes` of audio per hour.
- `transformer_sentiment` expects sentence level inputs. Input should not exceed 200 chars.
- `audio_classification_yamnet` expects shorter audios. Input should not exceed 30 seconds.


The request/response structure is explained [**here.**](https://fastdeploy.notai.tech/api)

**FILE input with CLI**
```bash
wget https://github.com/notAI-tech/fastDeploy/blob/master/cli/fastDeploy-file_client.py
chmod +x fastDeploy-file_client.py

# Single input
./fastDeploy-file_client.py --file PATH_TO_YOUR_IMAGE --url https://tech.notai.tech/efficientnet/b2/async --webhook https://fastdeploy.requestcatcher.com

# Client side batching
./fastDeploy-file_client.py --dir PATH_TO_FOLDER --ext wav --url https://tech.notai.tech/audio_classification/yamnet/async --webhook https://fastdeploy.requestcatcher.com
```

**File input python example**: (https://fastdeploy.notai.tech/api#request-type-file](https://fastdeploy.notai.tech/api#request-type-file)


**Async JSON with webhook example from bash**
```bash
curl -d '{"data": ["text_1", "text_2"], "webhook": "https://fastdeploy.requestcatcher.com"}' -H "Content-Type: application/json" "https://tech.notai.tech/deepsegment/en/async?api_key=API_KEY"
```

**Async JSON with webhook example from python**
```python
import requests

data = {"data": ["text_1", "text_2"], "webhook": "https://fastdeploy.requestcatcher.com"}

requests.post('https://tech.notai.tech/deepsegment/en/async', params={'api_key': API_KEY}, json=data).json()
```
