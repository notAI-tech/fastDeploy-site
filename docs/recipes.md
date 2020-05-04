---
layout: default
title: Recipes
nav_order: 2
permalink: /recipes
---

# Recipes
{: .no_toc }

We provide pre-built images for various Deep Learning models. Each recipie is a directory with the corresponding `predictor.py` and `example.pkl` 
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Building your own recipie/ deployment.
- A recipie (source_dir) is just a directory with your model's code and files.
- Apart from your model code and files, a recipie directory must contain `predictor.py`, `example.pkl`, and `requirements.txt`.
- If the recipie directory contains a bash script named `extras.sh`, it will be run at the start of build.

**requiremets.txt**
Example:
```
tensorflow==1.14.0
keras==2.2.4
numpy==1.16
```

**predictor.py and example.pkl**
Example
```python
from my_model import prediction_function

# prediction_function is the function you use to predict.

def predictor(inputs=[], batch_size=1):
    preds = []
    while True:
        batch_inputs = inputs[:batch_size]
        inputs = inputs[batch_size:]

        batch_preds = prediction_function(batch_inputs, ......)

        preds += batch_preds
    
    return preds

if __name__ == '__main__:
    import json
    import pickle
    # Sample inputs for your predictor function
    sample_inputs = ['....']

    # Verify that the inputs are json serializable
    json.dumps(sample_inputs)

    # Verify that predictor works as expected
    preds = predictor(sample_inputs)

    assert len(preds) == len(sample_inputs)

    # Verify that the predictions are json serializable
    json.dumps(preds)

    pickle.dump(sample_inputs, open('example.pkl', 'w'))
    
```

**Going through a relevant recipie's code might be helpful in understanding how `predictor.py` should be written.**


## CRAFT Text Detection:

**Arxiv**: [https://arxiv.org/abs/1904.01941](https://arxiv.org/abs/1904.01941)

**Based on**: [keras-ocr](https://github.com/faustomorales/keras-ocr/), [CRAFT-pytorch](https://github.com/clovaai/CRAFT-pytorch)

**View Code**: [On Github](https://github.com/notAI-tech/fastDeploy/tree/prototype/recipes/craft_text_detection)

CRAFT recipie uses the FILE format.

```


## 