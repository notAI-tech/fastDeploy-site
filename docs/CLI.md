---
layout: default
title: fastDeploy CLI
nav_order: 2
permalink: /cli
---

# CLI arguments and their description
{: .no_toc }

This section describes the arguments accepted by fastDeploy's CLI with examples.
{: .fs-6 .fw-300 }


- **build**: requires source_dir
- **source_dir** model/recipe source directory for building.

```bash
./fastDeploy.py --build temp_craft_text_detection --source_dir recipes/craft_text_detection/
```

- After build finishes, press `Ctrl + C` to exit and use docker commit to save your build.

```bash
# sudo might be required
docker commit temp_craft_text_detection craft_text_detection (or craft_text_detection:v1, ...)
```

- Backup docker image to your docker hub account

```bash
# sudo might be required
docker tag craft_text_detection dockerhub_username/repo_name:craft_text_detection
docker push dockerhub_username/repo_name:craft_text_detection
```

- **run**: runs a build.
- **name**: Optional name for the container.

```bash
./fastDeploy.py --run craft_text_detection:v1 (or name_of_recipe from --list_recipes)

# with --name

./fastDeploy.py --run craft_text_detection:v1 --name craft_text_detection
```

- **port**: Default:8080; the port on which the APIs run.

```
--port 8000
```
- **extra_config**: (If) Any environment variables.

```bash
--extra_config '{"VARIABLE_1": "VALUE"}'
```

- List of default arguments and their values.

|NAME                 | Default value| Description|
|:-------------------:|:------------:|:----------:|
|ONLY_ASYNC           | False        | if anything but empty, `/sync` will be disabled.|
|TIMEOUT              | 120          | `/sync` request timeout|
|WORKERS              | auto-calculated| Number of gunircorn workers. Suggested to leave it on auto.|
|CACHE                | 0.05 * free memory |memory cache limit|
|MAX_RAM_FILE_SIZE    |2 (MB)        |limit the file size that can be stored in CACHE |
|BATCH_SIZE           | auto-calculated| Maximum Batch size used for predictions |
|MAX_PER_CLIENT_BATCH | 0 (No limit)        | Maximum number of examples allowed in client batch. 0 for No limit|
|MAX_WAIT             | 0.2          | loop will wait for time_per_example * MAX_WAIT is batch_size is less than BATCH_SIZE |


- **verbose**: Prints corresponding docker commands.

```bash
--verbose
```
- **list_recipes**: Lists available pre-built recipes.

```bash
--list_recipes
```
