---
date: 2024-03-23
layout: zettel
category: 
tags:
  - data-streaming
---
- Append only logs are essentially the log-type data storage meaning the data can only be appended.
- Append only logs are not a new concepts (in data streaming applications) but were previously used in databases for change data capture (write ahead logs). These were used to make sure data was synced in database clusters with master and worker nodes
- Following are the characteristics of log-structured storage:
$multiflash
	- Logs are are often joined and merged
	- Logs file are often compacted (deleted) on the basis of age; meaning older files are deleted and newer file remains.
	- Log file are stored in different files because if they are stored in a single file their speed is limited by i/o.
