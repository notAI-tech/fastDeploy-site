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

- Running a recipe via CLI.
```bash
./fastDeploy.py --run RECIPE_NAME
```

- Source code for all the recipes is [here](https://github.com/notAI-tech/fastDeploy/tree/master/recipes).

# Text Detection in images

|Name                         |Description                             |Based On|extra_config| Input Type|
|:---------------------------:|:--------------------------------------:|:------:|:----------:|:---------:|
|craft_text_detection |Multi-lingual Text Detection in images |[keras-ocr](https://github.com/faustomorales/keras-ocr/), [CRAFT-pytorch](https://github.com/clovaai/CRAFT-pytorch)|N/A|FILE|

# Image Classification

|Name                         |Description                             |Based On|extra_config| Input Type|
|:---------------------------:|:--------------------------------------:|:------:|:----------:|:---------:|
|efficientnet_b0 |Imagenet Image classification |[EfficientNet](https://github.com/qubvel/efficientnet)|N/A|FILE|
|efficientnet_b2 |Imagenet Image classification |[EfficientNet](https://github.com/qubvel/efficientnet)|N/A|FILE|
|efficientnet_b4 |Imagenet Image classification |[EfficientNet](https://github.com/qubvel/efficientnet)|N/A|FILE|
|efficientnet_b7 |Imagenet Image classification |[EfficientNet](https://github.com/qubvel/efficientnet)|N/A|FILE|

|nudeclassifier |Sexual image classification |[NudeNet](https://github.com/bedapudi6788/NudeNet)|N/A|FILE|


# Sentence Splitting

|Name                         |Description                             |Based On|extra_config| Input Type|
|:---------------------------:|:--------------------------------------:|:------:|:----------:|:---------:|
|deepsegment_en |Split English text into sentences |[DeepSegment](https://github.com/bedapudi6788/deepsegment)|N/A|JSON|
|deepsegment_fr |Split French text into sentences  |[DeepSegment](https://github.com/bedapudi6788/deepsegment)|N/A|JSON|
|deepsegment_it |Split Italian text into sentences |[DeepSegment](https://github.com/bedapudi6788/deepsegment)|N/A|JSON|

# Summarization

|Name                         |Description                             |Based On|extra_config| Input Type|
|:---------------------------:|:--------------------------------------:|:------:|:----------:|:---------:|
|transformer_summarization  |English text summarization           |[Transformers](https://github.com/huggingface/transformers)|MAX_LEN (default: 0 for no limit)|JSON|

# Named Entity Recognition

|Name                         |Description                             |Based On|extra_config| Input Type|
|:---------------------------:|:--------------------------------------:|:------:|:----------:|:---------:|
|transformer_ner            |English Named Entity Recognition     |[Transformers](https://github.com/huggingface/transformers)|MAX_LEN (default: 0 for no limit)|JSON|

# Sentiment Analysis

|Name                         |Description                             |Based On|extra_config| Input Type|
|:---------------------------:|:--------------------------------------:|:------:|:----------:|:---------:|
|transformer_sentiment      |English Sentiment Analysis           |[Transformers](https://github.com/huggingface/transformers)|MAX_LEN (default: 0 for no limit)|JSON|

# Translation

|Name                         |Description                             |Based On|extra_config| Input Type|
|:---------------------------:|:--------------------------------------:|:------:|:----------:|:---------:|
|transformer_translation_en_to_fr  |English to French translation           |[Transformers](https://github.com/huggingface/transformers)|MAX_LEN (default: 0 for no limit)|JSON|

# Speech Recognition

|Name                         |Description                             |Based On|extra_config| Input Type|
|:---------------------------:|:--------------------------------------:|:------:|:----------:|:---------:|
|kaldi_vosk-en_us-small      |English speech recogniton           |[VOSK-api](https://github.com/alphacep/vosk-api/blob/master/doc/models.md)|MAX_WAV_LEN (default: 0 for no limit)|FILE|
|kaldi_vosk-en_us-aspire      |English speech recogniton           |[VOSK-api](https://github.com/alphacep/vosk-api/blob/master/doc/models.md)|MAX_WAV_LEN (default: 0 for no limit)|FILE|

# Audio Classification

|Name                         |Description                             |Based On|extra_config| Input Type|
|:---------------------------:|:--------------------------------------:|:------:|:----------:|:---------:|
|audio_classification_yamnet  |predicts 521 audio event classes        |[YAMNet](https://github.com/tensorflow/models/tree/master/research/audioset/yamnet)|N/A|FILE|



# Building your own recipe/ deployment.
- A recipe (source_dir) is just a directory with your model's code and files.
- Apart from your model code and files, a recipe directory must contain `predictor.py`, `example.pkl`, and `requirements.txt`.
- If the recipe directory contains a bash script named `extras.sh`, it will be run at the start of the build.

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

