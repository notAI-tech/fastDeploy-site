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

- We use `efficientnet_b4` (FILE input), `deepsegment_en` (JSON input) and `transformers_ner` (JSON input) recipes for our benchmarks.
- EfficientNet B4 is an image classifier CNN; DeepSegment is a sequence tagger BiLSTM+CRF.; Transformers NER is a sequence tagger transformer.

- **Batch Size**: indicates the client side batch size used in request to fastDeploy; (and) the batch size in model.predict call for native benchmark. 
- **Native**: Total time in seconds for native prediction for 8192 examples, averaged over 3 runs for a given `Batch Size`. This is simply the best inference throughput possible on the hardware. Note that we don't include disk read, preprocessing times in native.
- **fastDeploy**: Total time in seconds for fastDeploy prediction for 8192 examples, averaged over 3 runs for a given `Batch Size` and `Req Concurrency`. This includes data preprocessing, postprocessing, http overhead, model prediction times.
- Note: autocannon is used from localhost for benchmarking fastDeploy. i.e: The CPU is shared by fastDeploy and autocannon in this case.
- **Req Concurrency**: Max number of simultaneous reqeusts for benchmakring fastDeploy.

**As with any benchmark, you should take these numbers with a grain of salt. You should always run your own tests against your specific use case to discover what best suits your needs.**

**All the benchmarks are run with default fastDeploy config. Note that, by using case specific MX_WAIT, BATCH_SIZE config, the numbers can be improved.**



## DeepSegment English benchmark:
- Number of examples = 8192
- Benchmarked on a 12-core `Intel(R) Xeon(R) CPU E5-2690 v3 @ 2.60GHz` with 32 GB memory.

| Batch Size  | Native           |Req Concurrency| fastDeploy|
|:-----------:|:----------------:|:-------------:|:---------:|
|      1      |63.105387926101685|      1       |     79.06  |
|      1      |63.105387926101685|      16       |     30.05 |
|      1      |63.105387926101685|      256      |     27.1  |
|      1      |63.105387926101685|      2048     |     27.44 |
|      32     |6.848152160644531 |       1      |      8.06  |
|      32     |6.848152160644531 |       16      |      11.05|
|      32     |6.848152160644531 |       64      |       9.07|
|      32     |6.848152160644531 |       256     |       9.01|
|      128    |4.215409278869629 |    1         |   7.05   |
|      128    |4.215409278869629 |    16         |   9.26   |
|      128    |4.215409278869629 |    64         |    9.57  |

- In the worst possible scenario (only one request at a time), fastDeploy added a `0.001947632 sec/req` over head.
 


## Transformers NER benchmark:
- Number of examples = 1024
- Benchmarked on a 12-core `Intel(R) Xeon(R) CPU E5-2690 v3 @ 2.60GHz` with 32 GB memory.

## EfficientNet B4 benchmark:
- Number of examples = 512
- Benchmarked on a 12-core `Intel(R) Xeon(R) CPU E5-2690 v3 @ 2.60GHz` with 32 GB memory.
- Note that we don't include disk read, preprocessing times in native.

<!-- | Batch Size  | Native           |Req Concurrency| fastDeploy|
|:-----------:|:----------------:|:-------------:|:---------:|
|      1      |70.4393846988678  |      1       |     102.04 |
|      1      |70.4393846988678  |      8       |     96.05 |
|      1      |70.4393846988678  |      16      |     94.1  |
|      1      |70.4393846988678  |      64     |     94.44 |
|      2      |63.08684301376343 |      1      |      8.06  |
|      2      |63.08684301376343 |      8      |      11.05|
|      2      |63.08684301376343 |      16      |       9.07|
|      2      |63.08684301376343 |      64     |       9.01|
|      4     |61.65665125846863 |    1         |   7.05   |
|      4     |61.65665125846863 |    8         |   9.26   |
|      4     |61.65665125846863 |    16         |    9.57  |
|      4     |61.65665125846863 |    64         |    9.57  |
|      8     |63.688814640045166|    1         |    9.57  |
|      8     |63.688814640045166|    8         |    9.57  |
|      8     |63.688814640045166|    16         |    9.57  |
|      8     |63.688814640045166|    64         |    9.57  | -->