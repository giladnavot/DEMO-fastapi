---
title: User Class Overview
---
This document will cover the following aspects of the `User` class in the DEMO-fastapi repository:

1. What is the `User` class
2. Variables and functions in the `User` class
3. An example of how to use the `User` class

```mermaid
graph TD;
  User:::currentBaseStyle
User --> UserInDB

 classDef currentBaseStyle color:#000000,fill:#7CB9F4
```

# What is the User class

The `User` class in the DEMO-fastapi repository is a Pydantic model that represents a user in the application. It is used to validate the data of a user and to create a structured user object that can be used throughout the application.

<SwmSnippet path="/docs_src/security/tutorial004_an.py" line="40">

---

# Variables in the User class

The `username` variable is a required string that represents the username of the user.

```python
    username: str
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial004_an.py" line="41">

---

The `email` variable is an optional string that represents the email of the user. It defaults to `None` if not provided.

```python
    email: Union[str, None] = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial004_an.py" line="42">

---

The `full_name` variable is an optional string that represents the full name of the user. It defaults to `None` if not provided.

```python
    full_name: Union[str, None] = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial004_an.py" line="43">

---

The `disabled` variable is an optional boolean that represents whether the user is disabled or not. It defaults to `None` if not provided.

```python
    disabled: Union[bool, None] = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial004_an.py" line="46">

---

# Usage example

The `User` class is extended by the `UserInDB` class. The `UserInDB` class adds a `hashed_password` variable to the `User` class. This is an example of how the `User` class can be used to create more specific user models.

```python
class UserInDB(User):
    hashed_password: str

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="general-class"><sup>Powered by [Swimm](/)</sup></SwmMeta>
