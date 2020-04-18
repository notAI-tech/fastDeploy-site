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

### Quick start: Using a pre-built recipie.

1. Add Just the Docs to your Jekyll site's `_config.yml` as a [remote theme](https://blog.github.com/2017-11-29-use-any-theme-with-github-pages/)
```yaml
remote_theme: pmarsceill/just-the-docs
```
<small>You must have GitHub Pages enabled on your repo, one or more Markdown files, and a `_config.yml` file. [See an example repository](https://github.com/pmarsceill/jtd-remote)</small>

### : Building your recipie

1. Install the Ruby Gem
```bash
$ gem install just-the-docs
```
```yaml
# .. or add it to your your Jekyll site’s Gemfile
gem "just-the-docs"
```
2. Add Just the Docs to your Jekyll site’s `_config.yml`
```yaml
theme: "just-the-docs"
```
3. _Optional:_ Initialize search data (creates `search-data.json`)
```bash
$ bundle exec just-the-docs rake search:init
```
3. Run you local Jekyll server
```bash
$ jekyll serve
```
```bash
# .. or if you're using a Gemfile (bundler)
$ bundle exec jekyll serve
```
4. Point your web browser to [http://localhost:4000](http://localhost:4000)

If you're hosting your site on GitHub Pages, [set up GitHub Pages and Jekyll locally](https://help.github.com/en/articles/setting-up-your-github-pages-site-locally-with-jekyll) so that you can more easily work in your development environment.


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