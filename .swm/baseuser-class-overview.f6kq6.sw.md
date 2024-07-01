---
title: BaseUser Class Overview
---
This document will cover the `BaseUser` class in the DEMO-fastapi repository. We'll cover:

1. What is `BaseUser`
2. Variables and functions in `BaseUser`
3. An example of how to use `BaseUser`

```mermaid
graph TD;
  BaseUser:::currentBaseStyle
BaseUser --> UserIn

 classDef currentBaseStyle color:#000000,fill:#7CB9F4
```

# What is BaseUser

`BaseUser` is a class that represents a user in the codebase. It is used to store information about a user and is extended by other classes to add more specific user information.

<SwmSnippet path="/docs_src/response_model/tutorial003_01.py" line="10">

---

# Variables in BaseUser

The variable `username` is used to store the username of the user. It is a required string.

```python
    username: str
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/response_model/tutorial003_01.py" line="11">

---

The variable `email` is used to store the email of the user. It is a required string that must be a valid email.

```python
    email: EmailStr
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/response_model/tutorial003_01.py" line="12">

---

The variable `full_name` is used to store the full name of the user. It is an optional string.

```python
    full_name: Union[str, None] = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/response_model/tutorial003_01.py" line="15">

---

# Usage example

The `UserIn` class extends the `BaseUser` class. It adds a `password` variable to store the user's password. This is an example of how to use `BaseUser` to create a more specific user class.

```python
class UserIn(BaseUser):
    password: str
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="general-class"><sup>Powered by [Swimm](/)</sup></SwmMeta>
