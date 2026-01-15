---
paths: *.py
---

# Coding Guidelines

## Typing
- Use type hints for function arguments and return values.
- Use built-in types (e.g., `list`, `dict`) over legacy types (`List`, `Dict`) unless using generics from `typing`.
- Use `Optional[type]` for arguments that can be `None` only in Config files, not in other functions.
- Do it only when the type is not obvious from the assignment.

## Variable Naming
- Use descriptive, meaningful names for variables and functions.
- Use `snake_case` for variable, function, and method names.
- Use `UPPER_CASE` for constants.
- Use `CamelCase` for class names.
- Avoid single-letter variable names.
- For loops, use `ii`, `jj`, etc. instead of `i`, `j`.

## Best Practices
- Use spaces around operators and after commas.
- Use tabs for indentation.
- Avoid global variables.
- Prefer list comprehensions and generator expressions for simple transformations.
- Do not handle exceptions, except when absolutely necessary. When you do, handle them explicitly; do not use bare `except:` clauses.

## Imports
- At the top of the file, after any module comments or docstrings.
- Group imports in the following order: standard library, third-party, local.
- Use absolute imports whenever possible.
- Import only what you need; avoid wildcard imports (`from module import *`).

## Pytorch
- Use tensor operations instead of Python loops for performance, whenever possible.
- Regularly check tensor shapes and put comments after tensor operations indicating shape changes. Ex: `x = x.view(b, c, -1)  # b c h w -> b c (h w)`

