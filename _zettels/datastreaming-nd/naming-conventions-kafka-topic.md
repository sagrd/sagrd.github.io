---
date: 2024-08-27
layout: zettel
category: show
tags:
  - data-streaming
title: naming (conventions) of kafka topics
---
- The only enforced rules for topic names are that they must be less than 256 characters, consist only of alphanumeric characters (a-z, A-Z, 0-9), “.”, “_”, or “-”.
- There is no idiomatic or universally correct naming convention.
- Naming conventions can help reduce confusion, save time, and even increase reusability. [[Kafka]] consumers can consume many topics at once and they use regular expression for this.
- Example of a naming convention:
    - Consider starting with a namespace, like `com.udacity`
    - Consider segmenting on schema or model type, like `com.udacity.lesson`, where `lesson` is the model
    - Consider segmenting on event type, like `com.udacity.lesson.quiz_complete`, where `quiz_complete` is the event
    - 