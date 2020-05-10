---
layout: default
title: Best Practices
nav_order: 8
---

# Some notes about maximizing inference throughput.
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

===========INCOMPLETE===========

## Unused Resources are wasted Resources:
1. Our aim is to get the maximum inference throughput from any hardware.
2. For instance, take a look at the following predictor function.
```python
def predictor(in_examples=[], batch_size):
    # Converting JSON/ FILE PATH present in in_example to model inputs
    # preprocess is a example function,
    # which converts given input into features accepted by your model.
    # For instance, reading images and converting them to numpy arrays;
    # reading audio file and caluclating features etc.
    # Post process converts the model's numerical output space to outputs

    preds = []
    for in_example in in_examples:
        in_example = preprocess(in_example)
        model_pred = RESULT FROM PREDICTION
        model_pred = postprocess(model_pred)
        preds.append(model_pred)

    return model_preds
```

3. In the above example, we are not taking advantage of batch inference.
4. Batch inference is supported by most modern Deep Learning libraries (PyTorch, Keras, Tensorflow) and architectures.
5. **TL;DR: Use batching at your DL model's predict call whenever possible.**

```python
def predictor(in_examples=[], batch_size):
    in_examples = [preprocess(in_example) for in_example in in_examples]

    model_preds = MODEL.PREDICT(in_examples, ...)

    model_preds = [postprocess(pred) for pred in model_preds]

    return model_preds
```

6. The above `predictor` function uses batching for predictions.
7. As we are taking advantage of batching for the most expensive operation (inference) in predictor, this is very efficient compared to the above snippet.

8. If our preprocessing/ postprocessing functions are not in-expensive, using multiprocessing helps.

============TO BE UPDATED=========