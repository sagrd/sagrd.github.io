---
date: 2025-01-25
layout: zettel
category: show
tags:
  - airflow
title: Best practices for writing airflow dags
---
- Idempotency:
	- for a set input, running the program once has the same effect as running the program multiple times. A good idea is to make every task atomic and idempotent.
	- Idempotency paves the way for one of Airflow's most useful features: Retries
- Set retries:
	- It can be possible for tasks to be killed off unexpectedly. If this happens one might see a zombie process in airflow logs
	- Retries can be set at different levels with following precedence:
		- Tasks: Pass `retries` params to the task operator
		- DAGs: Include `retries` in DAG's `default_args` object
		- Deployments:  Set env variable `AIRFLOW__CORE__DEFAULT_TASK_RETRIES`
	- Setting retries to `2` will protect a task from most problems common to distributed environments.
- Using template fields, variables and macros
	- Bad practice: `yesterday = datetime.today() - timedelta(1)`
	- Good practice: `yesterday = {{ yesterday_ds_nodash }}`
		- because `datetime.today()` is relative to the current date, not the DAG execution date.
	- 