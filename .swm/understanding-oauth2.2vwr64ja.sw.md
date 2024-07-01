---
title: Understanding OAuth2
---
OAuth2, or Open Authorization 2, is a protocol that allows applications to obtain limited access to user accounts on an HTTP service. It works by delegating user authentication to the service that hosts the user account and authorizing third-party applications to access the user account. In the DEMO-fastapi repository, OAuth2 is implemented through various classes such as `OAuth2PasswordRequestForm`, `OAuth2PasswordBearer`, `OAuth2AuthorizationCodeBearer`, and `SecurityScopes`. These classes handle different OAuth2 flows like password flow and authorization code flow, and manage the collection of form data, token URLs, and scopes.

<SwmSnippet path="/fastapi/security/oauth2.py" line="16">

---

# OAuth2PasswordRequestForm Class

The `OAuth2PasswordRequestForm` class is a dependency class used to collect the `username` and `password` as form data for an OAuth2 password flow. It follows the OAuth2 specification, which dictates that for a password flow, the data should be collected using form data and should have the specific fields `username` and `password`.

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

<SwmSnippet path="/fastapi/security/oauth2.py" line="308">

---

# OAuth2 Class

The `OAuth2` class is the base class for OAuth2 authentication. An instance of it would be used as a dependency. All other OAuth2 classes inherit from it and customize it for each OAuth2 flow. It includes methods for initializing the OAuth2 model and handling authorization requests.

```python
class OAuth2(SecurityBase):
    """
    This is the base class for OAuth2 authentication, an instance of it would be used
    as a dependency. All other OAuth2 classes inherit from it and customize it for
    each OAuth2 flow.

    You normally would not create a new class inheriting from it but use one of the
    existing subclasses, and maybe compose them if you want to support multiple flows.

    Read more about it in the
    [FastAPI docs for Security](https://fastapi.tiangolo.com/tutorial/security/).
    """

    def __init__(
        self,
        *,
        flows: Annotated[
            Union[OAuthFlowsModel, Dict[str, Dict[str, Any]]],
            Doc(
                """
                The dictionary of OAuth2 flows.
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/security/oauth2.py" line="391">

---

# OAuth2PasswordBearer Class

The `OAuth2PasswordBearer` class is used for authentication using a bearer token obtained with a password. An instance of it would be used as a dependency. It includes methods for initializing the OAuth2 flows and handling authorization requests.

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

<SwmSnippet path="/fastapi/security/oauth2.py" line="152">

---

# OAuth2PasswordRequestFormStrict Class

The `OAuth2PasswordRequestFormStrict` class is similar to the `OAuth2PasswordRequestForm` class, but it requires the client to send the form field `grant_type` with the value `password`, which is required in the OAuth2 specification.

```python
class OAuth2PasswordRequestFormStrict(OAuth2PasswordRequestForm):
    """
    This is a dependency class to collect the `username` and `password` as form data
    for an OAuth2 password flow.

    The OAuth2 specification dictates that for a password flow the data should be
    collected using form data (instead of JSON) and that it should have the specific
    fields `username` and `password`.

    All the initialization parameters are extracted from the request.

    The only difference between `OAuth2PasswordRequestFormStrict` and
    `OAuth2PasswordRequestForm` is that `OAuth2PasswordRequestFormStrict` requires the
    client to send the form field `grant_type` with the value `"password"`, which
    is required in the OAuth2 specification (it seems that for no particular reason),
    while for `OAuth2PasswordRequestForm` `grant_type` is optional.

    Read more about it in the
    [FastAPI docs for Simple OAuth2 with Password and Bearer](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/).

    ## Example
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/security/oauth2.py" line="598">

---

# SecurityScopes Class

The `SecurityScopes` class is a special class that you can define in a parameter in a dependency to obtain the OAuth2 scopes required by all the dependencies in the same chain. This allows multiple dependencies to have different scopes, even when used in the same path operation.

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

# OAuth2 Authentication Classes

This section covers the main classes used for OAuth2 authentication in the FastAPI framework.

<SwmSnippet path="/fastapi/security/oauth2.py" line="16">

---

## OAuth2PasswordRequestForm

The `OAuth2PasswordRequestForm` class is a dependency class used to collect the `username` and `password` as form data for an OAuth2 password flow. It follows the OAuth2 specification which dictates that for a password flow, the data should be collected using form data and should have the specific fields `username` and `password`.

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

The `OAuth2PasswordBearer` class is used for the OAuth2 flow for authentication using a bearer token obtained with a password. An instance of it would be used as a dependency. It requires the URL to obtain the OAuth2 token, which would be the path operation that has `OAuth2PasswordRequestForm` as a dependency.

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

The `OAuth2AuthorizationCodeBearer` class is used for the OAuth2 flow for authentication using a bearer token obtained with an OAuth2 code flow. An instance of it would be used as a dependency. It requires the URL to obtain the OAuth2 token and optionally the URL to refresh the token and obtain a new one.

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
