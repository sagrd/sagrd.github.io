---
date: 2024-12-20
layout: zettel
category: show
tags:
  - "#python"
title: Generators in Python
---
Generators
   - Generators are a special type of iterator that yield items one at a time, allowing for lazy evaluation. This is particularly useful for large datasets, as it does not load the entire dataset into memory.
   - Example:

```
def count_up_to(max):
    count = 1
    while count <= max:
        yield count
        count += 1

for number in count_up_to(5):
    print(number)  # Output: 1, 2, 3, 4, 5
```
