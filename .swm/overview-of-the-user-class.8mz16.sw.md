---
title: Overview of the User Class
---
This document will cover the following topics related to the 'User' class in the DEMO-fastapi repository:

1. What is 'User'
2. Variables and functions in 'User'
3. Usage example of 'User'

```mermaid
graph TD;
  User:::currentBaseStyle
User --> UserInDB

 classDef currentBaseStyle color:#000000,fill:#7CB9F4
```

# What is User

The 'User' class in the DEMO-fastapi repository is a Pydantic model that represents a user in the system. It is used to validate the data of a user and to provide a clear model of what a user object should look like.

<SwmSnippet path="/docs_src/security/tutorial005_py310.py" line="50">

---

# Variables in User

The 'username' variable is a string that represents the username of the user.

```python
    username: str
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial005_py310.py" line="51">

---

The 'email' variable is an optional string that represents the email of the user.

```python
    email: str | None = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial005_py310.py" line="52">

---

The 'full_name' variable is an optional string that represents the full name of the user.

```python
    full_name: str | None = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial005_py310.py" line="53">

---

The 'disabled' variable is an optional boolean that represents whether the user is disabled or not.

```python
    disabled: bool | None = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial005_py310.py" line="56">

---

# Usage example

The 'User' class is used as a base class for the 'UserInDB' class. 'UserInDB' extends 'User' and adds a 'hashed_password' variable. This shows how you can extend the 'User' class to add more information for different use cases.

```python
class UserInDB(User):
    hashed_password: str

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="general-class"><sup>Powered by [Swimm](/)</sup></SwmMeta>
