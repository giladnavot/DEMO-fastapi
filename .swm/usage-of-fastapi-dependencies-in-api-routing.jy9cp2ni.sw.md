---
title: Usage of FastAPI Dependencies in API Routing
---
This document will cover how dependencies are utilized in routing the API in the DEMO-fastapi repository. We'll cover:

1. The role of dependencies in the APIRoute and APIRouter classes
2. How dependencies are used in the `__init__` function
3. The use of dependencies in the `add_api_route` and `api_route` functions.

<SwmSnippet path="/fastapi/routing.py" line="354">

---

# Dependencies in APIRoute and APIRouter

In the `APIRoute` class, dependencies are defined as a list in the `__init__` function. These dependencies are then used to create a `Dependant` object, which is used to manage the dependencies of the route.

```python
    def __init__(
        self,
        path: str,
        endpoint: Callable[..., Any],
        *,
        name: Optional[str] = None,
        dependencies: Optional[Sequence[params.Depends]] = None,
        dependency_overrides_provider: Optional[Any] = None,
    ) -> None:
        self.path = path
        self.endpoint = endpoint
        self.name = get_name(endpoint) if name is None else name
        self.dependencies = list(dependencies or [])
        self.path_regex, self.path_format, self.param_convertors = compile_path(path)
        self.dependant = get_dependant(path=self.path_format, call=self.endpoint)
        for depends in self.dependencies[::-1]:
            self.dependant.dependencies.insert(
                0,
                get_parameterless_sub_dependant(depends=depends, path=self.path_format),
            )

```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/routing.py" line="545">

---

In the `APIRouter` class, dependencies are defined as an optional sequence of `Depends` objects. These dependencies are applied to all the path operations in the router.

````python
class APIRouter(routing.Router):
    """
    `APIRouter` class, used to group *path operations*, for example to structure
    an app in multiple files. It would then be included in the `FastAPI` app, or
    in another `APIRouter` (ultimately included in the app).

    Read more about it in the
    [FastAPI docs for Bigger Applications - Multiple Files](https://fastapi.tiangolo.com/tutorial/bigger-applications/).

    ## Example

    ```python
    from fastapi import APIRouter, FastAPI

    app = FastAPI()
    router = APIRouter()


    @router.get("/users/", tags=["users"])
    async def read_users():
        return [{"username": "Rick"}, {"username": "Morty"}]
````

---

</SwmSnippet>

<SwmSnippet path="/fastapi/routing.py" line="354">

---

# Dependencies in the **init** function

In the `__init__` function of the `APIRoute` class, the `get_dependant` and `get_parameterless_sub_dependant` functions are used to manage the dependencies of the route. The `get_websocket_app` function is also used to manage dependencies in the context of a WebSocket app.

```python
    def __init__(
        self,
        path: str,
        endpoint: Callable[..., Any],
        *,
        name: Optional[str] = None,
        dependencies: Optional[Sequence[params.Depends]] = None,
        dependency_overrides_provider: Optional[Any] = None,
    ) -> None:
        self.path = path
        self.endpoint = endpoint
        self.name = get_name(endpoint) if name is None else name
        self.dependencies = list(dependencies or [])
        self.path_regex, self.path_format, self.param_convertors = compile_path(path)
        self.dependant = get_dependant(path=self.path_format, call=self.endpoint)
        for depends in self.dependencies[::-1]:
            self.dependant.dependencies.insert(
                0,
                get_parameterless_sub_dependant(depends=depends, path=self.path_format),
            )

```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/applications.py" line="1056">

---

# Dependencies in add_api_route and api_route

In the `add_api_route` function, dependencies are defined as an optional sequence of `Depends` objects. These dependencies are then passed to the `add_api_route` function of the router.

```python
    def add_api_route(
        self,
        path: str,
        endpoint: Callable[..., Coroutine[Any, Any, Response]],
        *,
        response_model: Any = Default(None),
        status_code: Optional[int] = None,
        tags: Optional[List[Union[str, Enum]]] = None,
        dependencies: Optional[Sequence[Depends]] = None,
        summary: Optional[str] = None,
        description: Optional[str] = None,
        response_description: str = "Successful Response",
        responses: Optional[Dict[Union[int, str], Dict[str, Any]]] = None,
        deprecated: Optional[bool] = None,
        methods: Optional[List[str]] = None,
        operation_id: Optional[str] = None,
        response_model_include: Optional[IncEx] = None,
        response_model_exclude: Optional[IncEx] = None,
        response_model_by_alias: bool = True,
        response_model_exclude_unset: bool = False,
        response_model_exclude_defaults: bool = False,
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/applications.py" line="1115">

---

In the `api_route` function, dependencies are defined as an optional sequence of `Depends` objects. These dependencies are then passed to the `add_api_route` function of the router.

```python
    def api_route(
        self,
        path: str,
        *,
        response_model: Any = Default(None),
        status_code: Optional[int] = None,
        tags: Optional[List[Union[str, Enum]]] = None,
        dependencies: Optional[Sequence[Depends]] = None,
        summary: Optional[str] = None,
        description: Optional[str] = None,
        response_description: str = "Successful Response",
        responses: Optional[Dict[Union[int, str], Dict[str, Any]]] = None,
        deprecated: Optional[bool] = None,
        methods: Optional[List[str]] = None,
        operation_id: Optional[str] = None,
        response_model_include: Optional[IncEx] = None,
        response_model_exclude: Optional[IncEx] = None,
        response_model_by_alias: bool = True,
        response_model_exclude_unset: bool = False,
        response_model_exclude_defaults: bool = False,
        response_model_exclude_none: bool = False,
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="follow-up"><sup>Powered by [Swimm](/)</sup></SwmMeta>
