---
date: 2024-02-27
layout: zettel
category: 
tags:
  - geo-distributed
  - article
link: https://minlanyu.seas.harvard.edu/writeup/eurosys18.pdf
article-name: Wide-Area Analytics with Multiple Resources
---

- Problem
	- Past approaches:
		- has been to locate map task in the sites with input data and placing reduce tasks there to minimize shuffle time.
			- based on assumption that all sites have infinite resources to run the job which is wrong.
		- only fraction of reduce task execute at a time due to constraints on compute resources
	- Approach/Intuition
	- Allocate multiple resources (compute and network slots) to analytics jobs with parallel tasks on geo-distributed systems with variability