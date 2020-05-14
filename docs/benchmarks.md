---
layout: default
title: Benchmarks
nav_order: 7
---

# Performance, Overhead benchmarks
{: .no_toc }

..... 
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

====INCOMPLETE=====

## Benchmakring process

- We use efficientnet_b2 (FILE input) and deepsegment_en (JSON input) recipes for our benchmarks.
- EfficientNet B2 is an image classifier CNN and DeepSegment is a sequence tagger BiLSTM+CRF.

- **Batch Size**: indicates the client side batch size used in request to fastDeploy; (and) the batch size in model.predict call for baseline benchmark. 
- **Baseline**: Total time in seconds for baseline prediction for 10000 examples, averaged over 3 runs for a given `Batch Size`.
- **fastDeploy**: Total time in seconds for fastDeploy prediction for 10000 examples, averaged over 3 runs for a given `Batch Size` and `Req Concurrency`.
- **Req Concurrency**: Max number of simultaneous reqeusts for benchmakring fastDeploy.
- **Overhead**: Overhead (in seconds) added by fastDeploy.

## Benchmakring scripts

- **DeepSegment**

```bash
# Install requirements.
pip install --upgrade deepsegment==2.3.1
pip install --upgrade tensorflow==1.14
pip install --upgrade keras==2.2.4
```

```python
from time import time
from deepsegment import DeepSegment

model = DeepSegment('en')

example = ["I was hungry i ordered a pizza and i went to the movies which movie did you go to i watched dark knight rises oh how was it it was a good movie yeah thought so"]

# Warmup
for _ in range(3):
    print(model.segment(example, batch_size=1)

# Expected result is [['I was hungry', 'i ordered a pizza and i went to the movies', 'which movie did you go to', 'i watched dark knight rises', 'oh how was it', 'it was a good movie', 'yeah thought so']]

in_data = list(example * 10000)

for batch_size in [1, 8, 32, 64, 128, 256, 512]:
    start = time()
    results = model.segment(in_data, batch_size)
    end = time()
    print(f'\nBatch Size:{batch_size}  Total Time:{end - start} per {len(in_data)} examples.')

```

## Benchmark Results

This section benchmarks the overhead added by fastDeploy in different scenarios.

| Recipe        | Batch Size  | Baseline   |Req Concurrency| fastDeploy| Overhead|
|:-------------:|:-----------:|:----------:|:-------------:|:---------:|:-------:|
|efficientnet_b2|             |            |               |           |         |
| deepsegment_en|             |            |               |           |         |
