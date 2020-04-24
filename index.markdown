---
layout: default
title: Quick start
nav_order: 1
description: "fastDeploy enables you to build production ready APIs for Deep Learning models."
permalink: /
---

# Focus on building models, not on deployments.
{: .fs-9 }

fastDeploy is a standardized serving solution with sane defaults, that enables you to deploy any ML/DL model as production ready, sync and async API(s) via containerization.
{: .fs-6 .fw-300 }

[Get started now](#getting-started){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 } [View it on GitHub](https://github.com/notAI-tech/fastDeploy){: .btn .fs-5 .mb-4 .mb-md-0 }

---

## Getting started

### Dependencies

fastDeploy's only requirement is [docker](https://docs.docker.com/install/).

### Quick start: Build the deployment via Web Interface.

**COMING SOON**

### : Build the deployment via fastDeploy CLI

fastDeploy's CLI is a simple, helpful wrapper over docker.
```bash
python fastDeploy.py --help

# Build local directory
python fastDeploy.py --name flair_ner --source_dir ../flair_ner_recipie_dir

# Build from download link (of zipped source dir/ recipie)
python fastDeploy.py --name flair_ner --zip_url DOWNLOADABLE_LINK
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