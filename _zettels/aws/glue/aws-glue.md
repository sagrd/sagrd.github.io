---
date: 2024-09-12
layout: zettel
category: show
tags:
  - "#aws"
  - "#glue"
title: About Aws Glue
---

- AWS Glue is fully managed serverless etl service
- Has capabilities of data integration via visual and code based interface

- Components of AWS Glue:
	- AWS Glue console:
		- Orchestrate ETL workflow
	- AWS Glue data catalogue:
		- Persistant metadata store
	- AWS Glue crawlers and classifiers:
		- Detect and infer schemas to store it in data catalog
	- AWS Glue ETL operation:
		- Automatic ETL code generation in Python or Scala
	- Streaming ETL in AWS Glue:
		- ETL operations in streaming data
	- AWS Glue Job System:
		- Enable to orchestrate the ETL workflow which can be scheduled or triggered based on events.
	
- Steps involved:
	- Define crawler to populate data catalogue
	- Create ETL Job
	- Generate / Write script for AWS Job
	- Run the job on demand and define scheduler or trigger
	- Extract data from DS, transform it and load it into data store

- Benefits:
	- Serverless
	- Automatic Schema Recognization
	- Code Autogeneration
	- Interface
	- Scalability: Can dynamically scale resources up and down
- 
- Drawbacks:
	- limited to python & scala programming language