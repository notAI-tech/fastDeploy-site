---
layout: default
title: Quickstart
nav_order: 1
description: "Deploy any DL/ ML inference pipelines with minimal extra code."
permalink: /
---

# ML/DL models -> scalable, efficient, and configurable API deployments.
{: .fs-9 }

Deploy DL/ ML inference pipelines with minimal extra code.
{: .fs-6 .fw-300 }

[Download CLI](https://raw.githubusercontent.com/notAI-tech/fastDeploy/master/cli/fastDeploy.py){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 } [View on GitHub](https://github.com/notAI-tech/fastDeploy){: .btn .fs-5 .mb-4 .mb-md-0 }

---


## Features:
  - Optimal batch size is estimated and inputs are automatically batched.
  - Prediction can be run in sync or async using `/sync` and `/async` endpoints.
  - Supports everything supported by Python; Tensorflow, Keras, Pytorch, MXNet, Kaldi ..
  - Minimal extra code: You don't need to write any fastDeploy specific code.

### Dependencies

[Docker](https://docs.docker.com/install/) is the only dependency.

### Quickstart: Run a pre-built fastDeploy recipe via CLI.

fastDeploy's CLI is a simple, helpful wrapper over docker.

- See the complete list of commands supported [here](./cli).
- Learn about the structure of source_dir [here](./recipes).
- List of API endpoints and request-response formats are detailed [here](./api).

```bash
# See all the arguments supported.
./fastDeploy.py --help

# Print list of available recipes with descriptions.
./fastDeploy.py --list_recipes

# Run a recipe (eg: craft_text_detection).
./fastDeploy.py --run craft_text_detection --name craft_text_detection_test_run
```


---

## About the project

fastDeploy is built by [notAI.tech](https://github.com/notAI-tech).

### License

fastDeploy is distributed by an [MIT license](https://github.com/notAI-tech/fastDeploy/blob/master/LICENSE).


### Contributing

When contributing to this repository, please first discuss the change you wish to make via [Github issue](https://github.com/notAI-tech/fastDeploy/issues)

#### This website is adapted by:

<ul class="list-style-none">
{% for contributor in site.github.contributors %}
  <li class="d-inline-block mr-1">
     <a href="{{ contributor.html_url }}"><img src="{{ contributor.avatar_url }}" width="32" height="32" alt="{{ contributor.login }}"/></a>
  </li>
{% endfor %}
</ul>

### Code of Conduct

notAI.tech is committed to fostering a welcoming community.

[View our Code of Conduct](https://github.com/notAI-tech/fastDeploy/tree/master/CODE_OF_CONDUCT.md) on our GitHub repository.