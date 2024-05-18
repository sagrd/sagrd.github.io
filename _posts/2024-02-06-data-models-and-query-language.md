---
layout: post
---

Data models are critical in software development, shaping how we tackle the problems we aim to solve. Here's a breakdown of the most prominent data models and their roles:
## Relational Model
- Popularity: Most widely known and used.
- Key Feature: Hides implementation details behind a clean interface.
- Adaptability: Generalizes well across diverse computing purposes.
- Handling Relationships:
	- One-to-Many:
		- Common approach: Separate table with foreign key reference.
		- SQL enhancements: Multi-valued data in a single row.
		- Less favorable: Encoded JSON or XML with application-level queries.
	- Many-to-One:
		- Easy referencing via IDs.
		- Efficient use of joins.
- Criticism:
	- Requires awkward translation between application code objects and database model.
	- ORM frameworks reduce but don’t eliminate overhead.
- Historical Impact:
	- Overpowered older hierarchical and network models.
	- Query optimizer facilitated adding new features to applications.

## NoSQL Databases
- Adoption Reasons:
	- Better scaling, including very high write throughput.
	- Free and open source.
	- Superior for specific query operations.
	- More dynamic and expressive data models.
- Coexistence:
	- Used alongside relational databases (Polyglot Persistence).
- Document-Oriented Databases:
	- One-to-Many:
		- Natively supports with better data locality.
		- Self-contained JSON structure.
	- Many-to-One:
		- Less efficient, requires application-level join simulation.
- Schema Flexibility:
	- Schema-on-read vs. relational model’s schema-on-write.
	- Easier to change and modify.
- Data Locality:
	- Documents need to be relatively small.
- Future Trends:
	- Hybrid models combining relational and document features.

## Query Languages
- SQL:
	- Attractive due to its declarative nature.
	- Specifies the pattern of the resulting data.
	- Easier to parallelize across multiple machines.
- MapReduce:
	- Low-level programming model for distributed execution.
	- Not exclusive for distributed query execution.
- Graph Data Model:
	- Suitable for data with many-to-many relationships.
	- Supports well-known algorithms and efficient querying with languages like Cypher.
	- Greater flexibility for application adaptation compared to network models.
