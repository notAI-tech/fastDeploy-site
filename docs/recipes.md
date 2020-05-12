---
layout: default
title: Recipes
nav_order: 4
permalink: /recipes
---

# Recipes
{: .no_toc }

We provide pre-built images for various Deep Learning models. Each recipe is a directory with the corresponding `predictor.py` and `example.pkl` 
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Building your own recipe/ deployment.
- A recipe (source_dir) is just a directory with your model's code and files.
- Apart from your model code and files, a recipe directory must contain `predictor.py`, `example.pkl`, and `requirements.txt`.
- If the recipe directory contains a bash script named `extras.sh`, it will be run at the start of build.

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
    while inputs:
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

    pickle.dump(sample_inputs, open('example.pkl', 'wb'))

```

**Going through a relevant recipe's code might be helpful in understanding how `predictor.py` should be written.**


## CRAFT Text Detection:

```bash
./fastDeploy.py --run craft_text_detection
```

**Arxiv**: [https://arxiv.org/abs/1904.01941](https://arxiv.org/abs/1904.01941)

**Based on**: [keras-ocr](https://github.com/faustomorales/keras-ocr/), [CRAFT-pytorch](https://github.com/clovaai/CRAFT-pytorch)

**View Code**: [On Github](https://github.com/notAI-tech/fastDeploy/tree/master/recipes/craft_text_detection)

CRAFT recipe uses the FILE format.



## DeepSegment_en/fr/it:

```bash
# English
./fastDeploy.py --run deepsegment_en

# French
./fastDeploy.py --run deepsegment_fr

# Italian
./fastDeploy.py --run deepsegment_it
```

**Arxiv**: N/A

**Based on**: [DeepSegment](https://github.com/bedapudi6788/deepsegment)

**View Code**: [On Github](https://github.com/notAI-tech/fastDeploy/tree/master/recipes/deepsegment)

DeepSegment recipe(s) uses the JSON format.


## HuggingFace Transformer_summarization/ner/sentiment

```bash
# Summarization
./fastDeploy.py --run transformer_summarization

# Named Entity Recognition
./fastDeploy.py --run transformer_ner

# Sentiment Analysis
./fastDeploy.py --run transformer_sentiment
```

**Arxiv**: N/A

**Based on**: [Transformers](https://github.com/huggingface/transformers)

**View Code**: [On Github](https://github.com/notAI-tech/fastDeploy/tree/master/recipes/huggingface_transformers)

Transformer recipe(s) uses the JSON format.


## NudeClassifier
```bash
./fastDeploy.py --run nudeclassifier
```

**Arxiv**: N/A

**Based on**: [NudeNet](https://github.com/bedapudi6788/NudeNet)

**View Code**: [On Github](https://github.com/notAI-tech/fastDeploy/tree/master/recipes/nudeclassifier)

## YamNet Audio Classification

```bash
./fastDeploy.py --run audioclassifier_yamnet
```

**Arxiv**: N/A

**Based on**: [yamnet](https://github.com/tensorflow/models/tree/master/research/audioset/yamnet)

**View Code**: [On Github](https://github.com/notAI-tech/fastDeploy/tree/master/recipes/audio_classification_yamnet)
