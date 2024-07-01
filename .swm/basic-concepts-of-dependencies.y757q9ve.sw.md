---
title: Basic Concepts of Dependencies
---
In the DEMO-fastapi repository, dependencies are used to manage and organize the different components of the application. They are implemented using the FastAPI framework's dependency injection system. This system allows for better code organization, reusability, and testing. Dependencies in this context are functions that return a value, which can be used in other parts of the application. They are defined using the Depends keyword in FastAPI, and can be included in the parameters of path operation functions. The FastAPI framework automatically resolves these dependencies, ensuring that each function receives the correct parameters.

<SwmSnippet path="/fastapi/dependencies/utils.py" line="241">

---

# Defining Dependencies

The `get_dependant` function is used to create a `Dependant` object, which represents a dependency. It takes in the path, the callable (function or class) that will be called when the dependency is resolved, and other optional parameters. It then analyzes the parameters of the callable to determine if they have any dependencies, and if so, it recursively creates `Dependant` objects for them.

```python
def get_dependant(
    *,
    path: str,
    call: Callable[..., Any],
    name: Optional[str] = None,
    security_scopes: Optional[List[str]] = None,
    use_cache: bool = True,
) -> Dependant:
    path_param_names = get_path_param_names(path)
    endpoint_signature = get_typed_signature(call)
    signature_params = endpoint_signature.parameters
    dependant = Dependant(
        call=call,
        name=name,
        path=path,
        security_scopes=security_scopes,
        use_cache=use_cache,
    )
    for param_name, param in signature_params.items():
        is_path_param = param_name in path_param_names
        type_annotation, depends, param_field = analyze_param(
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/dependencies/utils.py" line="524">

---

# Resolving Dependencies

The `solve_dependencies` function is used to resolve the dependencies of a `Dependant` object. It takes in a request, a `Dependant` object, and other optional parameters. It then iterates over the dependencies of the `Dependant` object, resolves them, and stores the results in a cache for future use. If a dependency has sub-dependencies, it recursively calls `solve_dependencies` to resolve them.

```python
async def solve_dependencies(
    *,
    request: Union[Request, WebSocket],
    dependant: Dependant,
    body: Optional[Union[Dict[str, Any], FormData]] = None,
    background_tasks: Optional[StarletteBackgroundTasks] = None,
    response: Optional[Response] = None,
    dependency_overrides_provider: Optional[Any] = None,
    dependency_cache: Optional[Dict[Tuple[Callable[..., Any], Tuple[str]], Any]] = None,
    async_exit_stack: AsyncExitStack,
) -> Tuple[
    Dict[str, Any],
    List[Any],
    Optional[StarletteBackgroundTasks],
    Response,
    Dict[Tuple[Callable[..., Any], Tuple[str]], Any],
]:
    values: Dict[str, Any] = {}
    errors: List[Any] = []
    if response is None:
        response = Response()
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/routing.py" line="1312">

---

# Using Dependencies

Dependencies are used in the path operation functions by including them in the function parameters. FastAPI will automatically resolve these dependencies before the function is called. In this example, the `get` function defines a path operation for the GET HTTP method. It includes dependencies in its parameters, and FastAPI will resolve these dependencies when a GET request is made to the specified path.

```python
    def get(
        self,
        path: Annotated[
            str,
            Doc(
                """
                The URL path to be used for this *path operation*.

                For example, in `http://example.com/items`, the path is `/items`.
                """
            ),
        ],
        *,
        response_model: Annotated[
            Any,
            Doc(
                """
                The type to use for the response.

                It could be any valid Pydantic *field* type. So, it doesn't have to
                be a Pydantic model, it could be other things, like a `list`, `dict`,
```

---

</SwmSnippet>

# Dependency Functions

This section will cover the main functions related to dependencies in the FastAPI framework.

<SwmSnippet path="/fastapi/dependencies/utils.py" line="103">

---

## get_param_sub_dependant

The `get_param_sub_dependant` function is used to get a sub-dependant based on the provided parameters. It calls the `get_sub_dependant` function.

```python
def get_param_sub_dependant(
    *,
    param_name: str,
    depends: params.Depends,
    path: str,
    security_scopes: Optional[List[str]] = None,
) -> Dependant:
    assert depends.dependency
    return get_sub_dependant(
        depends=depends,
        dependency=depends.dependency,
        path=path,
        name=param_name,
        security_scopes=security_scopes,
    )
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/dependencies/utils.py" line="127">

---

## get_sub_dependant

The `get_sub_dependant` function is used to get a sub-dependant based on the provided parameters. It checks if the dependency is a security scheme and calls the `get_dependant` function.

```python
def get_sub_dependant(
    *,
    depends: params.Depends,
    dependency: Callable[..., Any],
    path: str,
    name: Optional[str] = None,
    security_scopes: Optional[List[str]] = None,
) -> Dependant:
    security_requirement = None
    security_scopes = security_scopes or []
    if isinstance(depends, params.Security):
        dependency_scopes = depends.scopes
        security_scopes.extend(dependency_scopes)
    if isinstance(dependency, SecurityBase):
        use_scopes: List[str] = []
        if isinstance(dependency, (OAuth2, OpenIdConnect)):
            use_scopes = security_scopes
        security_requirement = SecurityRequirement(
            security_scheme=dependency, scopes=use_scopes
        )
    sub_dependant = get_dependant(
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/dependencies/utils.py" line="162">

---

## get_flat_dependant

The `get_flat_dependant` function is used to get a flat dependant, which is a dependant without any sub-dependencies. It recursively calls itself to flatten all sub-dependencies.

```python
def get_flat_dependant(
    dependant: Dependant,
    *,
    skip_repeats: bool = False,
    visited: Optional[List[CacheKey]] = None,
) -> Dependant:
    if visited is None:
        visited = []
    visited.append(dependant.cache_key)

    flat_dependant = Dependant(
        path_params=dependant.path_params.copy(),
        query_params=dependant.query_params.copy(),
        header_params=dependant.header_params.copy(),
        cookie_params=dependant.cookie_params.copy(),
        body_params=dependant.body_params.copy(),
        security_schemes=dependant.security_requirements.copy(),
        use_cache=dependant.use_cache,
        path=dependant.path,
    )
    for sub_dependant in dependant.dependencies:
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/dependencies/utils.py" line="241">

---

## get_dependant

The `get_dependant` function is used to get a dependant based on the provided parameters. It analyzes each parameter and adds it to the appropriate list in the dependant.

```python
def get_dependant(
    *,
    path: str,
    call: Callable[..., Any],
    name: Optional[str] = None,
    security_scopes: Optional[List[str]] = None,
    use_cache: bool = True,
) -> Dependant:
    path_param_names = get_path_param_names(path)
    endpoint_signature = get_typed_signature(call)
    signature_params = endpoint_signature.parameters
    dependant = Dependant(
        call=call,
        name=name,
        path=path,
        security_scopes=security_scopes,
        use_cache=use_cache,
    )
    for param_name, param in signature_params.items():
        is_path_param = param_name in path_param_names
        type_annotation, depends, param_field = analyze_param(
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/dependencies/utils.py" line="524">

---

## solve_dependencies

The `solve_dependencies` function is used to solve all dependencies for a given request. It iterates over all dependencies and sub-dependencies, and solves them by calling the appropriate functions.

```python
async def solve_dependencies(
    *,
    request: Union[Request, WebSocket],
    dependant: Dependant,
    body: Optional[Union[Dict[str, Any], FormData]] = None,
    background_tasks: Optional[StarletteBackgroundTasks] = None,
    response: Optional[Response] = None,
    dependency_overrides_provider: Optional[Any] = None,
    dependency_cache: Optional[Dict[Tuple[Callable[..., Any], Tuple[str]], Any]] = None,
    async_exit_stack: AsyncExitStack,
) -> Tuple[
    Dict[str, Any],
    List[Any],
    Optional[StarletteBackgroundTasks],
    Response,
    Dict[Tuple[Callable[..., Any], Tuple[str]], Any],
]:
    values: Dict[str, Any] = {}
    errors: List[Any] = []
    if response is None:
        response = Response()
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
