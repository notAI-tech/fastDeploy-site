---
layout: default
title: fastDeploy CLI
nav_order: 8
permalink: /cli
---

# CLI arguments and their description
{: .no_toc }

This section describes the arguments accepted by fastDeploy's CLI and their description.
{: .fs-6 .fw-300 }


# Args and Descriptions

- **build**: builds the deployment for the model/predictor at source_dir. requires source_dir
- **commit**: commits/saves the container built by `build`.
- **run**: runs a build.

## Optional:
- **port**: the port on which the APIs run.
- **extra_config**: (If) Any environment variables.
- **source_dir** model/recipie source directory for building.


# Building a Deployment:
```bash
./fastDeploy.py --build build_name --source_dir ../directory_path
```

```bash
docker run --name build_name --tmpfs /ramdisk 
```