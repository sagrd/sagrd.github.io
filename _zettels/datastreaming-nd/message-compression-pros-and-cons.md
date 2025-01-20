---
date: 2024-08-28
layout: zettel
category: show
tags:
  - data-streaming
title: pros and cons of message compression
---
See this [Cloudflare Blog Post](https://blog.cloudflare.com/squeezing-the-firehose/) for an excellent summary of compression type pros and cons.

|Algorithm|Pros|Cons|
|---|---|---|
|lz4|fast compression and decompression|not a high compression ratio|
|snappy|fast compression and decompression|not a high compression ratio|
|zstd|high compression ratio|not as fast as lz4 or snappy|
|gzip|ubiquitous, widely-supported|cpu-intensive, significantly slower than lz4 or snappy|
