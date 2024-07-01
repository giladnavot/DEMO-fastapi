---
title: Overview of the User Class
---
This document will cover the following aspects of the User class in the DEMO-fastapi repository:

1. What is User
2. Variables and functions in User
3. Usage example of User

```mermaid
graph TD;
  User:::currentBaseStyle
User --> UserInDB

 classDef currentBaseStyle color:#000000,fill:#7CB9F4
```

# What is User

The User class in the DEMO-fastapi repository is a Pydantic model that represents a user in the system. It is used to validate and serialize user data.

<SwmSnippet path="/docs_src/security/tutorial005.py" line="51">

---

# Variables in User

The `username` variable is a required string that represents the username of the user.

```python
    username: str
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial005.py" line="52">

---

The `email` variable is an optional string that represents the email of the user.

```python
    email: Union[str, None] = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial005.py" line="53">

---

The `full_name` variable is an optional string that represents the full name of the user.

```python
    full_name: Union[str, None] = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial005.py" line="54">

---

The `disabled` variable is an optional boolean that represents whether the user is disabled or not.

```python
    disabled: Union[bool, None] = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial005.py" line="57">

---

# Usage example

The User class is extended by the UserInDB class. The UserInDB class adds a `hashed_password` variable to the User class and represents a user in the database.

```python
class UserInDB(User):
    hashed_password: str

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="general-class"><sup>Powered by [Swimm](/)</sup></SwmMeta>
