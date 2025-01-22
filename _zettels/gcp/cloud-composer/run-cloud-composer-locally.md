---
date: 2025-12-10
layout: zettel
category: show
tags:
  - cloud-composer
  - gcp
  - airflow
title: Instructions for running cloud composer locally
---
- This throws error: https://cloud.google.com/composer/docs/composer-2/run-local-airflow-environments
- On macOS with Docker Desktop, check **Enable default docker socket in Settings -> Advanced section**. Check and if it doesn't work
- Change this on `setup.py` and reinstall
```dependencies = [
    "click>=7.0",
    "google-auth==2.27.*",
    "google-cloud-orchestration-airflow>=1.2.0",
    "google-cloud-artifact-registry>=1.2.0",
    "rich_click==1.4.0",
    "docker==7.*", #change this from 6
    "requests==2.31.0", #add this
]
```


- `composer-dev restart local-cc --port=8081`
- `composer-dev start local-cc  --port=8081`
- `composer-dev stop local-cc`