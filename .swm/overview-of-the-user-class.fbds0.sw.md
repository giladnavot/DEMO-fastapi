---
title: Overview of the User Class
---
This document will cover the `User` class in the DEMO-fastapi repository. We'll cover:

1. What is `User`
2. Variables and functions in `User`
3. Usage example of `User`

```mermaid
graph TD;
  User:::currentBaseStyle
User --> UserInDB

 classDef currentBaseStyle color:#000000,fill:#7CB9F4
```

# What is User

The `User` class in `docs_src/security/tutorial003_py310.py` is a Pydantic model that represents a user in the application. It is used to validate and store user data.

<SwmSnippet path="/docs_src/security/tutorial003_py310.py" line="33">

---

# Variables in User

The `username` variable is a string that stores the username of the user.

```python
    username: str
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial003_py310.py" line="34">

---

The `email` variable is an optional string that stores the email of the user.

```python
    email: str | None = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial003_py310.py" line="35">

---

The `full_name` variable is an optional string that stores the full name of the user.

```python
    full_name: str | None = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial003_py310.py" line="36">

---

The `disabled` variable is an optional boolean that indicates whether the user is disabled.

```python
    disabled: bool | None = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial003_py310.py" line="39">

---

# Usage example

`User` is used as a base class for `UserInDB`. `UserInDB` extends `User` and adds a `hashed_password` variable.

```python
class UserInDB(User):
    hashed_password: str
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="general-class"><sup>Powered by [Swimm](/)</sup></SwmMeta>
