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
    2. The app has three api end points. ```/sync```, ```/async``` and ```/result```.
    3. ```/sync``` accepts, writes the data (to cache/ disk), waits for the result to appear in cache, and returns it.
    4. ```/async``` accepts, writes the data (and extra params like webhook) and return the unique_id of that input.
    5. ```/result``` accepts the unique_id, returns the result if it exists.



---

## Choices and Reasons

To specify a page order, use the `nav_order` parameter in your pages' YAML front matter.

#### Example
{: .no_toc }

```yaml
---
layout: default
title: Customization
nav_order: 4
---
```

---

## Excluding pages

For specific pages that you do not wish to include in the main navigation, e.g. a 404 page or a landing page, use the `nav_exclude: true` parameter in the YAML front matter for that page.

#### Example
{: .no_toc }

```yaml
---
layout: default
title: 404
nav_exclude: true
---
```

---

## Pages with children

Sometimes you will want to create a page with many children (a section). First, it is recommended that you keep pages that are related in a directory together... For example, in these docs, we keep all of the written documentation in the `./docs` directory and each of the sections in subdirectories like `./docs/ui-components` and `./docs/utilities`. This gives us an organization like:

```
+-- ..
|-- (Jekyll files)
|
|-- docs
|   |-- ui-components
|   |   |-- index.md  (parent page)
|   |   |-- buttons.md
|   |   |-- code.md
|   |   |-- labels.md
|   |   |-- tables.md
|   |   +-- typography.md
|   |
|   |-- utilities
|   |   |-- index.md      (parent page)
|   |   |-- color.md
|   |   |-- layout.md
|   |   |-- responsive-modifiers.md
|   |   +-- typography.md
|   |
|   |-- (other md files, pages with no children)
|   +-- ..
|
|-- (Jekyll files)
+-- ..
```

On the parent pages, add this YAML front matter parameter:
-  `has_children: true` (tells us that this is a parent page)

#### Example
{: .no_toc }

```yaml
---
layout: default
title: UI Components
nav_order: 2
has_children: true
---
```

Here we're setting up the UI Components landing page that is available at `/docs/ui-components`, which has children and is ordered second in the main nav.

### Child pages
{: .text-gamma }

On child pages, simply set the `parent:` YAML front matter to whatever the parent's page title is and set a nav order (this number is now scoped within the section).

#### Example
{: .no_toc }

```yaml
---
layout: default
title: Buttons
parent: UI Components
nav_order: 2
---
```

The Buttons page appears as a child of UI Components and appears second in the UI Components section.

### Auto-generating Table of Contents

By default, all pages with children will automatically append a Table of Contents which lists the child pages after the parent page's content. To disable this auto Table of Contents, set `has_toc: false` in the parent page's YAML front matter.

#### Example
{: .no_toc }

```yaml
---
layout: default
title: UI Components
nav_order: 2
has_children: true
has_toc: false
---
```

### Children with children
{: .text-gamma }

Child pages can also have children (grandchildren). This is achieved by using a similar pattern on the child and grandchild pages.

1. Add the `has_children` attribute to the child
1. Add the `parent` and `grand_parent` attribute to the grandchild

#### Example
{: .no_toc }

```yaml
---
layout: default
title: Buttons
parent: UI Components
nav_order: 2
has_children: true
---
```

```yaml
---
layout: default
title: Buttons Child Page
parent: Buttons
grand_parent: UI Components
nav_order: 1
---
```

This would create the following navigation structure:

```
+-- ..
|
|-- UI Components
|   |-- ..
|   |
|   |-- Buttons
|   |   |-- Button Child Page
|   |
|   |-- ..
|
+-- ..
```

---

## Auxiliary Navigation

pass

#### Example
{: .no_toc }

```yaml
# Aux links for the upper right navigation
aux_links:
  "Just the Docs on GitHub":
    - "//github.com/pmarsceill/just-the-docs"
```

---

## In-page navigation with Table of Contents

To generate a Table of Contents on your docs pages, you can use the `{:toc}` method from Kramdown, immediately after an `<ol>` in Markdown. This will automatically generate an ordered list of anchor links to various sections of the page based on headings and heading levels. There may be occasions where you're using a heading and you don't want it to show up in the TOC, so to skip a particular heading use the `{: .no_toc }` CSS class.

#### Example
{: .no_toc }

```markdown
# Navigation Structure
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
```

This example skips the page name heading (`#`) from the TOC, as well as the heading for the Table of Contents itself (`##`) because it is redundant, followed by the table of contents itself.
