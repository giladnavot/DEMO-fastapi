---
title: >-
  Integration of Security Measures with FastAPIs Routers, Requests, and
  Responses
---
This document will cover the integration of security measures into FastAPI's components like routers, requests, and responses. We'll cover:

1. The role of the Security function
2. The use of OAuth2 class
3. The use of RedirectResponse
4. The use of APIRouter

<SwmSnippet path="/fastapi/param_functions.py" line="2280">

---

# The role of the Security function

The `Security` function in FastAPI is used to declare a security dependency. It can declare OAuth2 scopes that will be integrated with OpenAPI and the automatic UI docs. It takes a single 'dependable' callable (like a function). FastAPI will call this function for you.

```python
def Security(  # noqa: N802
    dependency: Annotated[
        Optional[Callable[..., Any]],
        Doc(
            """
            A "dependable" callable (like a function).

            Don't call it directly, FastAPI will call it for you, just pass the object
            directly.
            """
        ),
    ] = None,
    *,
    scopes: Annotated[
        Optional[Sequence[str]],
        Doc(
            """
            OAuth2 scopes required for the *path operation* that uses this Security
            dependency.

            The term "scope" comes from the OAuth2 specification, it seems to be
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/security/oauth2.py" line="308">

---

# The use of OAuth2 class

The `OAuth2` class is the base class for OAuth2 authentication. An instance of it would be used as a dependency. All other OAuth2 classes inherit from it and customize it for each OAuth2 flow. It includes the dictionary of OAuth2 flows, security scheme name and description, and a flag for automatic error handling.

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

<SwmSnippet path="/docs_src/custom_response/tutorial006b.py" line="2">

---

# The use of RedirectResponse

`RedirectResponse` is a part of FastAPI's responses module. It is used to handle HTTP redirections.

```python
from fastapi.responses import RedirectResponse
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/custom_request_and_route/tutorial003.py" line="4">

---

# The use of APIRouter

`APIRouter` is a part of FastAPI's routing system. It is used to declare routes in your application.

```python
from fastapi import APIRouter, FastAPI, Request, Response
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="follow-up"><sup>Powered by [Swimm](/)</sup></SwmMeta>
