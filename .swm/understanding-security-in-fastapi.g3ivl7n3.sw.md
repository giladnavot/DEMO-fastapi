---
title: Understanding Security in FastAPI
---
Security in the DEMO-fastapi repository refers to the mechanisms used to protect the API and its data. This includes authentication and authorization mechanisms, such as OAuth2 and HTTP Basic, which ensure that only authorized users can access certain resources. The security features are implemented using classes like `SecurityScopes` and `OAuth2` in the `fastapi/security` module. These classes provide functionalities like handling OAuth2 scopes and flows, and checking the HTTP Authorization header in requests.

<SwmSnippet path="/fastapi/security/http.py" line="103">

---

## HTTP Security

This line shows how to create an instance of the HTTP security scheme and use it as a dependency in `Depends()`. The same approach is used for other security schemes.

```python
    Create an instance object and use that object as the dependency in `Depends()`.
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/security/api_key.py" line="26">

---

## API Key Security

This line shows how to create an instance of the API Key security scheme and use it as a dependency in `Depends()`. The API Key security scheme does not define how to send the API key to the client, this needs to be handled separately.

```python
    Create an instance object and use that object as the dependency in `Depends()`.
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/security/oauth2.py" line="71">

---

## OAuth2 Security

This line refers to the OAuth2 security scheme. It mentions that the scheme is strict and if you want to be more permissive, you should use the `OAuth2PasswordRequestForm` dependency instead.

```python
                allows not passing it. If you want to enforce it, use instead the
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/security/open_id_connect_url.py" line="32">

---

## OpenID Connect URL Security

This line refers to the OpenID Connect URL security scheme. Like other schemes, an instance of this scheme is created and used as a dependency in `Depends()`.

```python
                Security scheme name.
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
