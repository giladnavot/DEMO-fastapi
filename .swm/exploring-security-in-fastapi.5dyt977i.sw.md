---
title: Exploring Security in FastAPI
---
Security in the DEMO-fastapi repository refers to the measures taken to protect the API endpoints. This is achieved through various classes and methods provided by the FastAPI framework. The `SecurityScopes` class, for instance, is used to define the OAuth2 scopes required by all the dependencies in the same chain. The `OAuth2` class is the base class for OAuth2 authentication and is used as a dependency. It is customized for each OAuth2 flow. The repository also includes utilities for handling HTTP Authorization headers.

<SwmSnippet path="/fastapi/security/http.py" line="103">

---

# HTTP Basic Authentication

Here, an instance of the HTTP Basic security scheme is created. This instance can then be used as a dependency in `Depends()` to apply HTTP Basic authentication to an endpoint.

```python
    Create an instance object and use that object as the dependency in `Depends()`.
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/security/api_key.py" line="26">

---

# API Key Authentication

This is an example of creating an instance of the API Key security scheme. Similar to the HTTP Basic scheme, this instance can be used as a dependency in `Depends()` to apply API Key authentication to an endpoint.

```python
    Create an instance object and use that object as the dependency in `Depends()`.
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/security/oauth2.py" line="71">

---

# OAuth2 Authentication

This is an example of using the OAuth2 security scheme. The comment indicates that this scheme is flexible and can be used in a permissive manner, allowing for optional authentication.

```python
                allows not passing it. If you want to enforce it, use instead the
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
