---
title: User Class Overview
---
This document will cover the User class in the DEMO-fastapi repository. We'll cover:

1. What the User class is and its purpose.
2. The variables and functions defined in the User class.
3. An example of how to use the User class in UserInDB.

```mermaid
graph TD;
  User:::currentBaseStyle
User --> UserInDB

 classDef currentBaseStyle color:#000000,fill:#7CB9F4
```

# What is User

The User class is a Pydantic model that represents a user in the application. It is used to validate the data of a user and to provide a clear model of what a user object should look like. This class is used throughout the application wherever user data is handled.

<SwmSnippet path="/docs_src/security/tutorial004_py310.py" line="38">

---

# Variables and functions

The variable `username` is a required string that represents the username of the user.

```python
    username: str
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial004_py310.py" line="39">

---

The variable `email` is an optional string that represents the email of the user. It can be None if the user does not have an email.

```python
    email: str | None = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial004_py310.py" line="40">

---

The variable `full_name` is an optional string that represents the full name of the user. It can be None if the user does not have a full name.

```python
    full_name: str | None = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial004_py310.py" line="41">

---

The variable `disabled` is an optional boolean that represents whether the user is disabled. It can be None if the user's disabled status is not known.

```python
    disabled: bool | None = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/security/tutorial004_py310.py" line="44">

---

# Usage example

The User class is extended by the UserInDB class. The UserInDB class adds a `hashed_password` variable to the User class. This is an example of how the User class can be extended to add more data to the user model.

```python
class UserInDB(User):
    hashed_password: str
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="general-class"><sup>Powered by [Swimm](/)</sup></SwmMeta>
