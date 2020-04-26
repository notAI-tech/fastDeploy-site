---
layout: default
title: Quick start
nav_order: 1
description: "fastDeploy enables you to build production ready APIs for Deep Learning models."
permalink: /
---

# ML/DL models -> scalable, efficient and configurable API deployments.
{: .fs-9 }

fastDeploy provides a convenient way to serve DL/ ML models with minimal extra code. 
{: .fs-6 .fw-300 }

[Download CLI](){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 } [View it on GitHub](https://github.com/notAI-tech/fastDeploy){: .btn .fs-5 .mb-4 .mb-md-0 }

---


## Features:
  - Optimal batch size is estimated and inputs are automatically batched.
  - Prediction can be run in sync or async using `/sync` and `/async` endpoints.
  - Supports everything supported by Python; Tensorflow, Keras, Pytorch, MXNet, Kaldi ..
  - Minimal extra code: You don't need to write any fastDeploy specific code.

### Dependencies

[Docker](https://docs.docker.com/install/) is the only dependency.

### Quick start: Build the deployment via Web Interface.

**COMING SOON**

### Quick start: Build the deployment via CLI.

fastDeploy's CLI is a simple, helpful wrapper over docker.

**See the complete list of commands supported [here]().**
```bash
# See the arguments supported.
./fastDeploy.py --help

# Build from directory.
./fastDeploy.py --build build_name --source_dir ../directory_path

# Commit your build.
./fastDeploy.py --commit build_name

# Run your build.
./fastDeploy.py --run build_name
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