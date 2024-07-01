---
title: ValidationException Overview
---
This document will cover the `ValidationException` class in the DEMO-fastapi repository. We'll cover:

1. What is `ValidationException`
2. Variables and functions in `ValidationException`
3. Usage example of `ValidationException`

```mermaid
graph TD;
  ValidationException:::currentBaseStyle
ValidationException --> RequestValidationError
ValidationException --> WebSocketRequestValidationError
ValidationException --> ResponseValidationError

 classDef currentBaseStyle color:#000000,fill:#7CB9F4
```

# What is ValidationException

`ValidationException` is a class in the `fastapi/exceptions.py` file. It is a custom exception class used to handle validation errors in the FastAPI framework. It is designed to store a sequence of errors that occur during the validation process.

<SwmSnippet path="/fastapi/exceptions.py" line="150">

---

# Variables and functions

The `__init__` function is the constructor for the `ValidationException` class. It takes a sequence of errors as an argument and assigns it to the `_errors` instance variable.

```python
    def __init__(self, errors: Sequence[Any]) -> None:
        self._errors = errors
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/exceptions.py" line="153">

---

The `errors` function is a method of the `ValidationException` class. It returns the sequence of errors stored in the `_errors` instance variable.

```python
    def errors(self) -> Sequence[Any]:
        return self._errors
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/exceptions.py" line="167">

---

# Usage example

`ResponseValidationError` is a subclass of `ValidationException`. It overrides the `__init__` method to accept an additional `body` argument and the `__str__` method to provide a custom string representation. This is an example of how `ValidationException` can be extended and used in different contexts.

```python
class ResponseValidationError(ValidationException):
    def __init__(self, errors: Sequence[Any], *, body: Any = None) -> None:
        super().__init__(errors)
        self.body = body

    def __str__(self) -> str:
        message = f"{len(self._errors)} validation errors:\n"
        for err in self._errors:
            message += f"  {err}\n"
        return message
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="general-class"><sup>Powered by [Swimm](/)</sup></SwmMeta>
