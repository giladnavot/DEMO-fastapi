---
title: Basic Concepts of Applications
---
Applications in the context of the DEMO-fastapi repository refer to instances of the FastAPI class. These instances serve as the main entry point for using FastAPI. They are responsible for setting up routing, middleware, exception handling, and other core functionalities of the FastAPI framework. Applications also provide methods for defining path operations (API endpoints), such as GET, POST, PUT, DELETE, etc. Additionally, they handle events like startup and shutdown, and generate the OpenAPI schema for the API.

<SwmSnippet path="/fastapi/applications.py" line="48">

---

# FastAPI Application

This is the definition of the FastAPI application class. It inherits from the Starlette class, which is an ASGI framework. The FastAPI class includes methods for defining routes, adding middleware, and handling events.

````python
class FastAPI(Starlette):
    """
    `FastAPI` app class, the main entrypoint to use FastAPI.

    Read more in the
    [FastAPI docs for First Steps](https://fastapi.tiangolo.com/tutorial/first-steps/).

    ## Example

    ```python
    from fastapi import FastAPI

    app = FastAPI()
    ```
    """

    def __init__(
        self: AppType,
        *,
````

---

</SwmSnippet>

<SwmSnippet path="/fastapi/applications.py" line="1056">

---

# Defining Routes

This is an example of how to define a route in a FastAPI application. The `add_api_route` method takes a path and an endpoint function, along with optional parameters for the response model, status code, tags, dependencies, and more.

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

<SwmSnippet path="/fastapi/applications.py" line="4497">

---

# Adding Middleware

This is an example of how to add middleware to a FastAPI application. The `middleware` method takes a middleware type and returns a decorator that can be used to wrap a middleware function.

````python
    def middleware(
        self,
        middleware_type: Annotated[
            str,
            Doc(
                """
                The type of middleware. Currently only supports `http`.
                """
            ),
        ],
    ) -> Callable[[DecoratedCallable], DecoratedCallable]:
        """
        Add a middleware to the application.

        Read more about it in the
        [FastAPI docs for Middleware](https://fastapi.tiangolo.com/tutorial/middleware/).

        ## Example

        ```python
        import time
````

---

</SwmSnippet>

<SwmSnippet path="/fastapi/applications.py" line="4476">

---

# Handling Events

This is an example of how to handle events in a FastAPI application. The `on_event` method takes an event type and returns a decorator that can be used to wrap an event handler function.

```python
    def on_event(
        self,
        event_type: Annotated[
            str,
            Doc(
                """
                The type of event. `startup` or `shutdown`.
                """
            ),
        ],
    ) -> Callable[[DecoratedCallable], DecoratedCallable]:
        """
        Add an event handler for the application.

        `on_event` is deprecated, use `lifespan` event handlers instead.

        Read more about it in the
        [FastAPI docs for Lifespan Events](https://fastapi.tiangolo.com/advanced/events/#alternative-events-deprecated).
        """
        return self.router.on_event(event_type)
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
