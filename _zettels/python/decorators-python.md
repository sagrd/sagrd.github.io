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
