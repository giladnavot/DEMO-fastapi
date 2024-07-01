---
title: Overview of the User Class
---
This document will cover the User class in the DEMO-fastapi repository. We'll cover:

1. What is the User class
2. Variables and functions in the User class
3. An example of how to use the User class.

```mermaid
graph TD;
  User:::currentBaseStyle
User --> UserInDB

 classDef currentBaseStyle color:#000000,fill:#7CB9F4
```

# What is User

The User class is a Pydantic model that represents a user in the application. It is used to validate the data of a user and to create instances of a user with specific attributes.

<SwmSnippet path="/docs_src/security/tutorial004.py" line="39">

---

# Variables in User

The `username` variable is a required string that represents the username of the user.

```python
    username: str
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial004.py" line="40">

---

The `email` variable is an optional string that represents the email of the user. It can be None.

```python
    email: Union[str, None] = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial004.py" line="41">

---

The `full_name` variable is an optional string that represents the full name of the user. It can be None.

```python
    full_name: Union[str, None] = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial004.py" line="42">

---

The `disabled` variable is an optional boolean that represents whether the user is disabled. It can be None.

```python
    disabled: Union[bool, None] = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial004.py" line="45">

---

# Usage example

The User class is extended by the UserInDB class. The UserInDB class adds a `hashed_password` variable to the User class. This is an example of how the User class can be used to create a new class with additional attributes.

```python
class UserInDB(User):
    hashed_password: str
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="general-class"><sup>Powered by [Swimm](/)</sup></SwmMeta>
