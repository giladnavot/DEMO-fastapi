---
title: UserBase Class Overview
---
This document will cover the `UserBase` class from the `docs_src/extra_models/tutorial002.py` file in the DEMO-fastapi repository. We will discuss:

1. What is `UserBase`.
2. The variables and functions defined in `UserBase`.
3. An example of how `UserBase` is used in `UserIn`.

```mermaid
graph TD;
  UserBase:::currentBaseStyle
UserBase --> UserInDB
UserBase --> UserIn
UserBase --> UserOut

 classDef currentBaseStyle color:#000000,fill:#7CB9F4
```

# What is UserBase

`UserBase` is a class that serves as a base model for user-related classes in the FastAPI application. It is used to define the common attributes that all user-related classes should have.

<SwmSnippet path="/docs_src/extra_models/tutorial002.py" line="10">

---

# Variables in UserBase

The `username` variable is a string that stores the username of the user.

```python
    username: str
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/extra_models/tutorial002.py" line="11">

---

The `email` variable is an instance of `EmailStr` from the `pydantic` library, which validates that the input is a valid email address.

```python
    email: EmailStr
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/extra_models/tutorial002.py" line="12">

---

The `full_name` variable is a string that stores the full name of the user. It is optional and can be `None`.

```python
    full_name: Union[str, None] = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/extra_models/tutorial002.py" line="15">

---

# Usage example

`UserBase` is used as a base class for `UserIn`. `UserIn` inherits all the variables from `UserBase` and adds a `password` variable.

```python
class UserIn(UserBase):
    password: str
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="general-class"><sup>Powered by [Swimm](/)</sup></SwmMeta>
