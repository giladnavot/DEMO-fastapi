---
title: User Class Overview
---
This document will cover the `User` class in the DEMO-fastapi repository. We'll cover:

1. What the `User` class is.
2. The variables and functions defined in the `User` class.
3. An example of how to use the `User` class.

```mermaid
graph TD;
  User:::currentBaseStyle
User --> UserInDB

 classDef currentBaseStyle color:#000000,fill:#7CB9F4
```

# What is User

The `User` class is a Pydantic model that represents a user in the application. It is used to validate the data of a user and to provide a structured way to handle user data.

<SwmSnippet path="/docs_src/security/tutorial003_an_py310.py" line="35">

---

# Variables in User

The `username` variable is a required string that represents the username of the user.

```python
    username: str
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial003_an_py310.py" line="36">

---

The `email` variable is an optional string that represents the email of the user. It defaults to `None` if not provided.

```python
    email: str | None = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial003_an_py310.py" line="37">

---

The `full_name` variable is an optional string that represents the full name of the user. It defaults to `None` if not provided.

```python
    full_name: str | None = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial003_an_py310.py" line="38">

---

The `disabled` variable is an optional boolean that represents whether the user is disabled or not. It defaults to `None` if not provided.

```python
    disabled: bool | None = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial003_an_py310.py" line="41">

---

# Usage example

The `UserInDB` class is an example of how to use the `User` class. It extends the `User` class and adds a `hashed_password` variable.

```python
class UserInDB(User):
    hashed_password: str
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="general-class"><sup>Powered by [Swimm](/)</sup></SwmMeta>
