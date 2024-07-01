---
title: Overview of OAuth2
---
OAuth2, or Open Authorization 2, is a protocol that allows applications to obtain limited access to user accounts on an HTTP service. It works by delegating user authentication to the service that hosts the user account and authorizing third-party applications to access the user account. OAuth2 provides authorization flows for web and desktop applications, and mobile devices.

In the DEMO-fastapi repo, OAuth2 is implemented through several classes and functions. The `OAuth2PasswordRequestForm` class is a dependency that collects the `username` and `password` as form data for an OAuth2 password flow. The `OAuth2` class is the base class for OAuth2 authentication, and all other OAuth2 classes inherit from it and customize it for each OAuth2 flow.

The `OAuth2PasswordBearer` class is an OAuth2 flow for authentication using a bearer token obtained with a password. The `OAuth2AuthorizationCodeBearer` class is an OAuth2 flow for authentication using a bearer token obtained with an OAuth2 code flow. The `SecurityScopes` class is a special class that you can define in a parameter in a dependency to obtain the OAuth2 scopes required by all the dependencies in the same chain.

<SwmSnippet path="/fastapi/security/oauth2.py" line="16">

---

# OAuth2PasswordRequestForm

The `OAuth2PasswordRequestForm` class is a dependency that collects the `username` and `password` as form data for an OAuth2 password flow. It follows the OAuth2 specification, which requires that data for a password flow be collected using form data and that it should have the specific fields `username` and `password`.

````python
class OAuth2PasswordRequestForm:
    """
    This is a dependency class to collect the `username` and `password` as form data
    for an OAuth2 password flow.

    The OAuth2 specification dictates that for a password flow the data should be
    collected using form data (instead of JSON) and that it should have the specific
    fields `username` and `password`.

    All the initialization parameters are extracted from the request.

    Read more about it in the
    [FastAPI docs for Simple OAuth2 with Password and Bearer](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/).

    ## Example

    ```python
    from typing import Annotated

    from fastapi import Depends, FastAPI
    from fastapi.security import OAuth2PasswordRequestForm
````

---

</SwmSnippet>

<SwmSnippet path="/fastapi/security/oauth2.py" line="391">

---

# OAuth2PasswordBearer

The `OAuth2PasswordBearer` class is used for the OAuth2 password flow, which involves authentication using a bearer token obtained with a password. An instance of this class would be used as a dependency in a FastAPI route.

```python
class OAuth2PasswordBearer(OAuth2):
    """
    OAuth2 flow for authentication using a bearer token obtained with a password.
    An instance of it would be used as a dependency.

    Read more about it in the
    [FastAPI docs for Simple OAuth2 with Password and Bearer](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/).
    """

    def __init__(
        self,
        tokenUrl: Annotated[
            str,
            Doc(
                """
                The URL to obtain the OAuth2 token. This would be the *path operation*
                that has `OAuth2PasswordRequestForm` as a dependency.
                """
            ),
        ],
        scheme_name: Annotated[
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/security/oauth2.py" line="488">

---

# OAuth2AuthorizationCodeBearer

The `OAuth2AuthorizationCodeBearer` class is used for the OAuth2 authorization code flow, which involves authentication using a bearer token obtained with an OAuth2 code. An instance of this class would be used as a dependency in a FastAPI route.

```python
class OAuth2AuthorizationCodeBearer(OAuth2):
    """
    OAuth2 flow for authentication using a bearer token obtained with an OAuth2 code
    flow. An instance of it would be used as a dependency.
    """

    def __init__(
        self,
        authorizationUrl: str,
        tokenUrl: Annotated[
            str,
            Doc(
                """
                The URL to obtain the OAuth2 token.
                """
            ),
        ],
        refreshUrl: Annotated[
            Optional[str],
            Doc(
                """
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/security/oauth2.py" line="598">

---

# SecurityScopes

The `SecurityScopes` class is used to obtain the OAuth2 scopes required by all the dependencies in the same chain. This allows multiple dependencies to have different scopes, even when used in the same path operation.

```python
class SecurityScopes:
    """
    This is a special class that you can define in a parameter in a dependency to
    obtain the OAuth2 scopes required by all the dependencies in the same chain.

    This way, multiple dependencies can have different scopes, even when used in the
    same *path operation*. And with this, you can access all the scopes required in
    all those dependencies in a single place.

    Read more about it in the
    [FastAPI docs for OAuth2 scopes](https://fastapi.tiangolo.com/advanced/security/oauth2-scopes/).
    """

    def __init__(
        self,
        scopes: Annotated[
            Optional[List[str]],
            Doc(
                """
                This will be filled by FastAPI.
                """
```

---

</SwmSnippet>

# OAuth2 Functions

OAuth2 in FastAPI

<SwmSnippet path="/fastapi/security/oauth2.py" line="16">

---

## OAuth2PasswordRequestForm

The `OAuth2PasswordRequestForm` class is a dependency used to collect the `username` and `password` as form data for an OAuth2 password flow. It follows the OAuth2 specification which requires the data to be collected using form data and to have the specific fields `username` and `password`.

````python
class OAuth2PasswordRequestForm:
    """
    This is a dependency class to collect the `username` and `password` as form data
    for an OAuth2 password flow.

    The OAuth2 specification dictates that for a password flow the data should be
    collected using form data (instead of JSON) and that it should have the specific
    fields `username` and `password`.

    All the initialization parameters are extracted from the request.

    Read more about it in the
    [FastAPI docs for Simple OAuth2 with Password and Bearer](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/).

    ## Example

    ```python
    from typing import Annotated

    from fastapi import Depends, FastAPI
    from fastapi.security import OAuth2PasswordRequestForm
````

---

</SwmSnippet>

<SwmSnippet path="/fastapi/security/oauth2.py" line="391">

---

## OAuth2PasswordBearer

The `OAuth2PasswordBearer` class is used for the OAuth2 authentication flow using a bearer token obtained with a password. An instance of it would be used as a dependency.

```python
class OAuth2PasswordBearer(OAuth2):
    """
    OAuth2 flow for authentication using a bearer token obtained with a password.
    An instance of it would be used as a dependency.

    Read more about it in the
    [FastAPI docs for Simple OAuth2 with Password and Bearer](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/).
    """

    def __init__(
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/security/oauth2.py" line="488">

---

## OAuth2AuthorizationCodeBearer

The `OAuth2AuthorizationCodeBearer` class is used for the OAuth2 authentication flow using a bearer token obtained with an OAuth2 code flow. An instance of it would be used as a dependency.

```python
class OAuth2AuthorizationCodeBearer(OAuth2):
    """
    OAuth2 flow for authentication using a bearer token obtained with an OAuth2 code
    flow. An instance of it would be used as a dependency.
    """

    def __init__(
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
