---
layout: default
title: Architecture
nav_order: 5
---

# Some notes about the architecture of fastDeploy
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Design
![alt text](https://i.imgur.com/y6x4znY.png)


fastDeploy has two major components.

1. **loop :** the (computationally heavy) prediction loop.

    1. At startup, fastDeploy initializes the user supplied predictor function and estimates the optimal batch size for maximum inference throughput.
    2. After startup, the predictor waits for any inputs to appear, and processes them in batches if possible.

2. **app :** the API server that handles the requests. 

    1. Once the predictor is intialized, maximum parallelsim required (for API server) is estimated based on the batch size and number of CPU cores available.
    2. The app has three api end points. `/sync`, `/async` and `/result`.
    3. `/sync` accepts, writes the data (to cache/ disk), waits for the result to appear in cache, and returns it.
    4. `/async` accepts, writes the data (and extra params like webhook) and return the unique_id of that input.
    5. `/result` accepts the unique_id, returns the result if it exists.



---

## Choices and reasoning

1. fastDeploy is designed for stable and efficient inference. The model in a loop approach guarantees maximum possible inference throughput.

2. This modular approach enables us to replace other non-python dependant modules if required. For example, we can replace the current API server
(falcon + gevent) with golang or node based servers easily. 

3. Request/ response state handling, extras such as webhooks, are done independently via a index maintained in memory, and does not affect the inference performance.

## Advantages of this design

1. fastDeploy is an end-to-end serving solution for any type of model that can benefit from batching.
    1. For example, to deploy a image classification model via tensorflow serving, image pre-processing steps have to performed separately.
    2. this requires you to have different code for training and inference.
    3. fastDeploy serves the entite Deep Learning system, including the lightweight preprocessing steps required.

2. Features: supports sync, async apis, webhooks and file, json inputs, client side batching, server side batching.

3. Supports all deep learning toolkits. (PyTorch, Tensorflow, Keras, Kaldi ..  all support batching.)

3. Well tested and benchmarked.
    1. By design, fastDeploy's serving performance will always be more than sequential predictions.
    2. In all of our benchmarks, fastDeploy is significantly faster than tensorflow serving.

4. Recipies.
    1. We provide fastDeploy builds for various popular deep learning based libraries.
    2. Most of the general use-cases are covered in our recipies and can be used as starting point for your builds.

5. Training to Production pipelining as fast as possible.
    1. With fastDeploy, you can put your latest DL model in production in just two commands.
    2. Once built, the build image (docker image) can be re-used on any machine without re-installing or re-downloading the requirements.



## Disadvantages

This design has two obvious disadvantages.

1. docker supports `--tmpfs` only on linux. This means, fastDeploy's `/sync` will be very slow on mac and windows.
    1. Because of this, fastDeploy is essentially limited to linux.
    2. Note that, `/async` will work on all platforms as expected.

2. Horizontal Scaling and `/async`.
    1. Both `async`, `sync` work with horizontal and vertical scaling. But, `async` should only be used with webhooks if horizontally scaling.
    2. This is because, in `async` processing, the result is returned in a separate API call.
    3. This problem can simply be solved by running a api that acts as a webhook listner.
