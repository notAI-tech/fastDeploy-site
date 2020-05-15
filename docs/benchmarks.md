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

- We use `efficientnet_b2` (FILE input), `deepsegment_en` (JSON input) and `transformers_ner` (JSON input) recipes for our benchmarks.
- EfficientNet B2 is an image classifier CNN and DeepSegment is a sequence tagger BiLSTM+CRF.

- **Batch Size**: indicates the client side batch size used in request to fastDeploy; (and) the batch size in model.predict call for native benchmark. 
- **Native**: Total time in seconds for native prediction for 8192 examples, averaged over 3 runs for a given `Batch Size`. This is simply the best inference throughput possible on the hardware.
- **fastDeploy**: Total time in seconds for fastDeploy prediction for 8192 examples, averaged over 3 runs for a given `Batch Size` and `Req Concurrency`.
- **Req Concurrency**: Max number of simultaneous reqeusts for benchmakring fastDeploy.

## Benchmakring scripts

- **DeepSegment English**: 
- **EfficientNet B2**: 
- **Transformers NER**: 


## Benchmark Results

All benchmarks are run with 8192 examples.

| Recipe        | Batch Size  | Native           |Req Concurrency| fastDeploy|
|:-------------:|:-----------:|:----------------:|:-------------:|:---------:|
|efficientnet_b2|             |                  |               |           |           |
| deepsegment_en|      1      |63.105387926101685|      1       |     79.06  |
| deepsegment_en|      1      |63.105387926101685|      16       |     30.05 |
| deepsegment_en|      1      |63.105387926101685|      256      |     27.1  |
| deepsegment_en|      1      |63.105387926101685|      2048     |     27.44 |

| deepsegment_en|      32     |6.848152160644531 |       1      |      8.06  |
| deepsegment_en|      32     |6.848152160644531 |       16      |      11.05|
| deepsegment_en|      32     |6.848152160644531 |       64      |       9.07|
| deepsegment_en|      32     |6.848152160644531 |       256     |       9.01|

| deepsegment_en|      128    |4.215409278869629 |    1         |   7.05   |
| deepsegment_en|      128    |4.215409278869629 |    16         |   9.26   |
| deepsegment_en|      128    |4.215409278869629 |    64         |    9.57  |


