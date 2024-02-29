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

- Summary of what the paper says and does, in your words:
	- Problem
		- Past approaches:
			- has been to locate map task in the sites with input data and placing reduce tasks there to minimize shuffle time.
				- based on assumption that all sites have infinite resources to run the job which is wrong.
			- only fraction of reduce task execute at a time due to constraints on compute resources
	- Approach/Intuition
		- Allocate multiple resources (compute and network slots) to analytics jobs with parallel tasks on geo-distributed systems with variability
	- methods, conclusions as stated by the authors
	- What did they thought of their own paper
- Summary of what you thought of the paper:
	- Is it fundamentally sound? 
	- Does it uncover anything useful? 
	- Did they take shortcuts? 
	- Would you have done something differently? 
	- Did they miss an important experiment that would have made it more clear?
- Citations of interests
- Important figures