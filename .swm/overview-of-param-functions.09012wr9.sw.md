---
title: Overview of Param functions
---
Param functions in FastAPI are used to declare and validate parameters in API routes. They include functions like `Path`, `Query`, `Header`, `Cookie`, `Body`, `Form`, `File`, `Depends`, and `Security`. These functions provide a way to define the type, validation, serialization, and documentation information of parameters. They are used in route operation functions to extract and validate data from requests.

For example, the `Path` function is used to declare path parameters with validation, the `Query` function is used for query parameters, and the `Body` function is used for request body parameters. The `Depends` function is used to declare dependencies, and the `Security` function is used to declare security dependencies.

Each of these functions takes various arguments that allow you to define the behavior and validation of the parameter. For instance, you can set a default value, specify if a parameter is required, set validation rules, and more.

These param functions are integral to FastAPI's request handling and validation system, allowing for robust and flexible API design.

<SwmSnippet path="/fastapi/param_functions.py" line="11">

---

# Path Param Function

The `Path` function is used to declare path parameters. It takes various arguments to customize the behavior of the parameter. For example, `gt` and `lt` can be used to specify that the parameter value should be greater than or less than a certain value.

```python
def Path(  # noqa: N802
    default: Annotated[
        Any,
        Doc(
            """
            Default value if the parameter field is not set.

            This doesn't affect `Path` parameters as the value is always required.
            The parameter is available only for compatibility.
            """
        ),
    ] = ...,
    *,
    default_factory: Annotated[
        Union[Callable[[], Any], None],
        Doc(
            """
            A callable to generate the default value.

            This doesn't affect `Path` parameters as the value is always required.
            The parameter is available only for compatibility.
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/param_functions.py" line="339">

---

# Query Param Function

The `Query` function is used to declare query parameters. Similar to `Path`, it also takes various arguments to customize the behavior of the parameter.

```python
def Query(  # noqa: N802
    default: Annotated[
        Any,
        Doc(
            """
            Default value if the parameter field is not set.
            """
        ),
    ] = Undefined,
    *,
    default_factory: Annotated[
        Union[Callable[[], Any], None],
        Doc(
            """
            A callable to generate the default value.

            This doesn't affect `Path` parameters as the value is always required.
            The parameter is available only for compatibility.
            """
        ),
    ] = _Unset,
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/param_functions.py" line="1263">

---

# Body Param Function

The `Body` function is used to declare body parameters. It has an additional `embed` argument which, when set to `True`, expects the parameter in a JSON body as a key instead of being the JSON body itself.

```python
def Body(  # noqa: N802
    default: Annotated[
        Any,
        Doc(
            """
            Default value if the parameter field is not set.
            """
        ),
    ] = Undefined,
    *,
    default_factory: Annotated[
        Union[Callable[[], Any], None],
        Doc(
            """
            A callable to generate the default value.

            This doesn't affect `Path` parameters as the value is always required.
            The parameter is available only for compatibility.
            """
        ),
    ] = _Unset,
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/param_functions.py" line="1906">

---

# File Param Function

The `File` function is used to declare file parameters. The file data is expected in the request body as form data.

```python
def File(  # noqa: N802
    default: Annotated[
        Any,
        Doc(
            """
            Default value if the parameter field is not set.
            """
        ),
    ] = Undefined,
    *,
    default_factory: Annotated[
        Union[Callable[[], Any], None],
        Doc(
            """
            A callable to generate the default value.

            This doesn't affect `Path` parameters as the value is always required.
            The parameter is available only for compatibility.
            """
        ),
    ] = _Unset,
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/param_functions.py" line="959">

---

# Cookie Param Function

The `Cookie` function is used to declare cookie parameters. The cookie data is expected in the `Cookie` header of the request.

```python
def Cookie(  # noqa: N802
    default: Annotated[
        Any,
        Doc(
            """
            Default value if the parameter field is not set.
            """
        ),
    ] = Undefined,
    *,
    default_factory: Annotated[
        Union[Callable[[], Any], None],
        Doc(
            """
            A callable to generate the default value.

            This doesn't affect `Path` parameters as the value is always required.
            The parameter is available only for compatibility.
            """
        ),
    ] = _Unset,
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/param_functions.py" line="2220">

---

# Depends Param Function

The `Depends` function is used to declare dependencies. It takes a callable (like a function) which FastAPI will call to resolve the dependency.

```python
def Depends(  # noqa: N802
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
    use_cache: Annotated[
        bool,
        Doc(
            """
            By default, after a dependency is called the first time in a request, if
            the dependency is declared again for the rest of the request (for example
            if the dependency is needed by several dependencies), the value will be
            re-used for the rest of the request.
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/param_functions.py" line="2280">

---

# Security Param Function

The `Security` function is similar to `Depends`, but it can also declare OAuth2 scopes that will be integrated with OpenAPI and the automatic UI docs.

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

# Param Functions in FastAPI

This section will cover the main Param functions used in FastAPI.

<SwmSnippet path="/fastapi/param_functions.py" line="11">

---

## Path

The `Path` function is used to declare and validate path parameters. It supports validation options such as minimum and maximum length, pattern matching, and more.

```python
def Path(  # noqa: N802
    default: Annotated[
        Any,
        Doc(
            """
            Default value if the parameter field is not set.

            This doesn't affect `Path` parameters as the value is always required.
            The parameter is available only for compatibility.
            """
        ),
    ] = ...,
    *,
    default_factory: Annotated[
        Union[Callable[[], Any], None],
        Doc(
            """
            A callable to generate the default value.

            This doesn't affect `Path` parameters as the value is always required.
            The parameter is available only for compatibility.
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/param_functions.py" line="339">

---

## Query

The `Query` function is used to declare and validate query parameters. It supports similar validation options as `Path`.

```python
def Query(  # noqa: N802
    default: Annotated[
        Any,
        Doc(
            """
            Default value if the parameter field is not set.
            """
        ),
    ] = Undefined,
    *,
    default_factory: Annotated[
        Union[Callable[[], Any], None],
        Doc(
            """
            A callable to generate the default value.

            This doesn't affect `Path` parameters as the value is always required.
            The parameter is available only for compatibility.
            """
        ),
    ] = _Unset,
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/param_functions.py" line="1263">

---

## Body

The `Body` function is used to declare and validate request body parameters. It supports complex data types and nested models.

```python
def Body(  # noqa: N802
    default: Annotated[
        Any,
        Doc(
            """
            Default value if the parameter field is not set.
            """
        ),
    ] = Undefined,
    *,
    default_factory: Annotated[
        Union[Callable[[], Any], None],
        Doc(
            """
            A callable to generate the default value.

            This doesn't affect `Path` parameters as the value is always required.
            The parameter is available only for compatibility.
            """
        ),
    ] = _Unset,
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/param_functions.py" line="2220">

---

## Depends

The `Depends` function is used to declare dependencies, which can be other Param functions, or any callable that returns a value. FastAPI will automatically resolve these dependencies when handling a request.

```python
def Depends(  # noqa: N802
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
    use_cache: Annotated[
        bool,
        Doc(
            """
            By default, after a dependency is called the first time in a request, if
            the dependency is declared again for the rest of the request (for example
            if the dependency is needed by several dependencies), the value will be
            re-used for the rest of the request.
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/param_functions.py" line="2280">

---

## Security

The `Security` function is similar to `Depends`, but it also supports declaring OAuth2 scopes for the operation. This is useful for integrating with OpenAPI and the automatic UI docs.

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

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
