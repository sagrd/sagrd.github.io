---
date: 2024-03-27
layout: zettel
tags:
  - python
category: show
link: https://github.com/dabeaz-course/python-mastery
article-name: Advanced Python Mastery
---
-  Decorators
   - Decorators are a powerful tool that allow you to modify the behavior of functions or methods. They can be used to add functionality before or after the wrapped function is executed.
   - Example:
```
def decorator_function(original_function):
    def wrapper_function():
        print("Wrapper executed before {}".format(original_function.__name__))
        return original_function()
    return wrapper_function

@decorator_function
def display():
    return "Display function executed."

print(display())  # Output: Wrapper executed before display; Display function executed.
```
- Generators
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

- Context Managers
   - Context managers help in resource management by properly allocating and releasing system resources. The `with` statement is a common way to implement context management.
   - Example:
```
with open("myfile.txt", "w") as file:
    file.write("Hello World!")

# Using 'with' automatically closes the file after the block's execution.
```