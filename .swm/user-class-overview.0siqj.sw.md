---
title: User Class Overview
---
This document will cover the `User` class in the DEMO-fastapi repository. We'll cover:

1. What the `User` class is and its purpose.
2. The variables and functions defined in the `User` class.
3. An example of how to use the `User` class.

```mermaid
graph TD;
  User:::currentBaseStyle
User --> UserInDB

 classDef currentBaseStyle color:#000000,fill:#7CB9F4
```

# What is User

The `User` class is a Pydantic model that represents a user in the application. It is used to validate and serialize user data.

<SwmSnippet path="/docs_src/nosql_databases/tutorial001.py" line="25">

---

# Variables in User

The `username` variable is a string that stores the username of the user.

```python
    username: str
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/nosql_databases/tutorial001.py" line="26">

---

The `email` variable is an optional string that stores the email of the user.

```python
    email: Union[str, None] = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/nosql_databases/tutorial001.py" line="27">

---

The `full_name` variable is an optional string that stores the full name of the user.

```python
    full_name: Union[str, None] = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/nosql_databases/tutorial001.py" line="28">

---

The `disabled` variable is an optional boolean that stores whether the user is disabled.

```python
    disabled: Union[bool, None] = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/nosql_databases/tutorial001.py" line="31">

---

# Usage example

The `User` class is extended by the `UserInDB` class. `UserInDB` adds a `type` and `hashed_password` variable to the `User` class.

```python
class UserInDB(User):
    type: str = USERPROFILE_DOC_TYPE
    hashed_password: str
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="general-class"><sup>Powered by [Swimm](/)</sup></SwmMeta>
