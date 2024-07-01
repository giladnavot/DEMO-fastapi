---
title: Getting started with Param functions
---
Param functions in FastAPI are used to declare and validate request parameters. They include `Path`, `Query`, `Header`, `Cookie`, `Body`, `Form`, `File`, `Depends`, and `Security`. These functions are used to extract data from different parts of the request, perform validation, and document the parameters in the OpenAPI schema. They also support advanced features like dependencies, security scopes, and more.

<SwmSnippet path="/fastapi/param_functions.py" line="11">

---

# Path function

The `Path` function is used to declare and validate path parameters. It takes several arguments that specify the validation rules and metadata for the parameter. The `default` argument is used to specify the default value if the parameter is not provided in the request. Other arguments like `gt`, `ge`, `lt`, `le` are used to specify constraints on the value of the parameter.

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

# Query function

The `Query` function is used to declare and validate query parameters. It works similarly to the `Path` function, but it is used for parameters in the query string of the URL.

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

# Body function

The `Body` function is used to declare and validate parameters in the request body. It also takes several arguments that specify the validation rules and metadata for the parameter.

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

# File function

The `File` function is used to declare and validate file uploads. It works similarly to the `Body` function, but it is used for file upload fields in the request body.

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

# Cookie function

The `Cookie` function is used to declare and validate cookies. It works similarly to the `Query` function, but it is used for cookies in the request.

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

<SwmSnippet path="/fastapi/param_functions.py" line="643">

---

# Header function

The `Header` function is used to declare and validate HTTP headers. It works similarly to the `Query` function, but it is used for headers in the request.

```python
def Header(  # noqa: N802
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

# Depends function

The `Depends` function is used to declare dependencies. It takes a callable that will be called to provide the value of the dependency. The `use_cache` argument controls whether the result of the callable is cached for the duration of the request.

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

# Security function

The `Security` function is used to declare security dependencies. It works similarly to the `Depends` function, but it also takes a `scopes` argument that specifies the OAuth2 scopes required for the operation.

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

# Param Functions

This section will cover the main functions used to define parameters in FastAPI.

<SwmSnippet path="/fastapi/param_functions.py" line="11">

---

## Path

The `Path` function is used to declare a path parameter for a path operation. It takes several parameters such as default, default_factory, alias, alias_priority, and others. The function returns a `params.Path` object.

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

The `Query` function is used to declare a query parameter. It takes similar parameters to the `Path` function and returns a `params.Query` object.

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

<SwmSnippet path="/fastapi/param_functions.py" line="643">

---

## Header

The `Header` function is used to declare a header parameter. It takes similar parameters to the `Path` function and returns a `params.Header` object.

```python
def Header(  # noqa: N802
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

## Cookie

The `Cookie` function is used to declare a cookie parameter. It takes similar parameters to the `Path` function and returns a `params.Cookie` object.

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

<SwmSnippet path="/fastapi/param_functions.py" line="1263">

---

## Body

The `Body` function is used to declare a body parameter. It takes similar parameters to the `Path` function and returns a `params.Body` object.

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

<SwmSnippet path="/fastapi/param_functions.py" line="1592">

---

## Form

The `Form` function is used to declare a form parameter. It takes similar parameters to the `Path` function and returns a `params.Form` object.

```python
def Form(  # noqa: N802
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

## File

The `File` function is used to declare a file parameter. It takes similar parameters to the `Path` function and returns a `params.File` object.

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

<SwmSnippet path="/fastapi/param_functions.py" line="2220">

---

## Depends

The `Depends` function is used to declare a dependency. It takes a dependency callable and a use_cache parameter. The function returns a `params.Depends` object.

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

The `Security` function is used to declare a security dependency. It takes a dependency callable, scopes, and a use_cache parameter. The function returns a `params.Security` object.

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
