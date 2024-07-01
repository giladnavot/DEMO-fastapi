---
title: Understanding Params in FastAPI
---
<SwmSnippet path="/fastapi/params.py" line="21">

---

# Param class

The `Param` class is the base class for all types of parameters. It defines the common attributes and methods for all parameters, such as their default value, validation rules, and how they should be included in the OpenAPI schema.

```python
class Param(FieldInfo):
    in_: ParamTypes

    def __init__(
        self,
        default: Any = Undefined,
        *,
        default_factory: Union[Callable[[], Any], None] = _Unset,
        annotation: Optional[Any] = None,
        alias: Optional[str] = None,
        alias_priority: Union[int, None] = _Unset,
        # TODO: update when deprecating Pydantic v1, import these types
        # validation_alias: str | AliasPath | AliasChoices | None
        validation_alias: Union[str, None] = None,
        serialization_alias: Union[str, None] = None,
        title: Optional[str] = None,
        description: Optional[str] = None,
        gt: Optional[float] = None,
        ge: Optional[float] = None,
        lt: Optional[float] = None,
        le: Optional[float] = None,
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/params.py" line="221">

---

# Query class

The `Query` class is used for parameters that are passed in the query string of the URL. It extends the `Param` class and sets the `in_` attribute to `ParamTypes.query`.

```python
class Query(Param):
    in_ = ParamTypes.query

    def __init__(
        self,
        default: Any = Undefined,
        *,
        default_factory: Union[Callable[[], Any], None] = _Unset,
        annotation: Optional[Any] = None,
        alias: Optional[str] = None,
        alias_priority: Union[int, None] = _Unset,
        # TODO: update when deprecating Pydantic v1, import these types
        # validation_alias: str | AliasPath | AliasChoices | None
        validation_alias: Union[str, None] = None,
        serialization_alias: Union[str, None] = None,
        title: Optional[str] = None,
        description: Optional[str] = None,
        gt: Optional[float] = None,
        ge: Optional[float] = None,
        lt: Optional[float] = None,
        le: Optional[float] = None,
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/params.py" line="135">

---

# Path class

The `Path` class is used for parameters that are part of the URL path. It extends the `Param` class and sets the `in_` attribute to `ParamTypes.path`.

```python
class Path(Param):
    in_ = ParamTypes.path

    def __init__(
        self,
        default: Any = ...,
        *,
        default_factory: Union[Callable[[], Any], None] = _Unset,
        annotation: Optional[Any] = None,
        alias: Optional[str] = None,
        alias_priority: Union[int, None] = _Unset,
        # TODO: update when deprecating Pydantic v1, import these types
        # validation_alias: str | AliasPath | AliasChoices | None
        validation_alias: Union[str, None] = None,
        serialization_alias: Union[str, None] = None,
        title: Optional[str] = None,
        description: Optional[str] = None,
        gt: Optional[float] = None,
        ge: Optional[float] = None,
        lt: Optional[float] = None,
        le: Optional[float] = None,
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/params.py" line="305">

---

# Header class

The `Header` class is used for parameters that are passed in the HTTP headers. It extends the `Param` class and sets the `in_` attribute to `ParamTypes.header`.

```python
class Header(Param):
    in_ = ParamTypes.header

    def __init__(
        self,
        default: Any = Undefined,
        *,
        default_factory: Union[Callable[[], Any], None] = _Unset,
        annotation: Optional[Any] = None,
        alias: Optional[str] = None,
        alias_priority: Union[int, None] = _Unset,
        # TODO: update when deprecating Pydantic v1, import these types
        # validation_alias: str | AliasPath | AliasChoices | None
        validation_alias: Union[str, None] = None,
        serialization_alias: Union[str, None] = None,
        convert_underscores: bool = True,
        title: Optional[str] = None,
        description: Optional[str] = None,
        gt: Optional[float] = None,
        ge: Optional[float] = None,
        lt: Optional[float] = None,
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/params.py" line="391">

---

# Cookie class

The `Cookie` class is used for parameters that are passed in cookies. It extends the `Param` class and sets the `in_` attribute to `ParamTypes.cookie`.

```python
class Cookie(Param):
    in_ = ParamTypes.cookie

    def __init__(
        self,
        default: Any = Undefined,
        *,
        default_factory: Union[Callable[[], Any], None] = _Unset,
        annotation: Optional[Any] = None,
        alias: Optional[str] = None,
        alias_priority: Union[int, None] = _Unset,
        # TODO: update when deprecating Pydantic v1, import these types
        # validation_alias: str | AliasPath | AliasChoices | None
        validation_alias: Union[str, None] = None,
        serialization_alias: Union[str, None] = None,
        title: Optional[str] = None,
        description: Optional[str] = None,
        gt: Optional[float] = None,
        ge: Optional[float] = None,
        lt: Optional[float] = None,
        le: Optional[float] = None,
```

---

</SwmSnippet>

# Parameter Handling Functions

This section will cover the functions related to handling different types of parameters in the API.

<SwmSnippet path="/fastapi/params.py" line="21">

---

## Param Class

The `Param` class is the base class for all types of parameters. It includes common attributes such as `default`, `alias`, `title`, `description`, and `deprecated`. The `__init__` method is used to initialize these attributes.

```python
class Param(FieldInfo):
    in_: ParamTypes

    def __init__(
        self,
        default: Any = Undefined,
        *,
        default_factory: Union[Callable[[], Any], None] = _Unset,
        annotation: Optional[Any] = None,
        alias: Optional[str] = None,
        alias_priority: Union[int, None] = _Unset,
        # TODO: update when deprecating Pydantic v1, import these types
        # validation_alias: str | AliasPath | AliasChoices | None
        validation_alias: Union[str, None] = None,
        serialization_alias: Union[str, None] = None,
        title: Optional[str] = None,
        description: Optional[str] = None,
        gt: Optional[float] = None,
        ge: Optional[float] = None,
        lt: Optional[float] = None,
        le: Optional[float] = None,
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/params.py" line="135">

---

## Path Class

The `Path` class is a subclass of `Param` and is used for path parameters. It overrides the `in_` attribute to `ParamTypes.path`.

```python
class Path(Param):
    in_ = ParamTypes.path

    def __init__(
        self,
        default: Any = ...,
        *,
        default_factory: Union[Callable[[], Any], None] = _Unset,
        annotation: Optional[Any] = None,
        alias: Optional[str] = None,
        alias_priority: Union[int, None] = _Unset,
        # TODO: update when deprecating Pydantic v1, import these types
        # validation_alias: str | AliasPath | AliasChoices | None
        validation_alias: Union[str, None] = None,
        serialization_alias: Union[str, None] = None,
        title: Optional[str] = None,
        description: Optional[str] = None,
        gt: Optional[float] = None,
        ge: Optional[float] = None,
        lt: Optional[float] = None,
        le: Optional[float] = None,
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/params.py" line="221">

---

## Query Class

The `Query` class is a subclass of `Param` and is used for query parameters. It overrides the `in_` attribute to `ParamTypes.query`.

```python
class Query(Param):
    in_ = ParamTypes.query

    def __init__(
        self,
        default: Any = Undefined,
        *,
        default_factory: Union[Callable[[], Any], None] = _Unset,
        annotation: Optional[Any] = None,
        alias: Optional[str] = None,
        alias_priority: Union[int, None] = _Unset,
        # TODO: update when deprecating Pydantic v1, import these types
        # validation_alias: str | AliasPath | AliasChoices | None
        validation_alias: Union[str, None] = None,
        serialization_alias: Union[str, None] = None,
        title: Optional[str] = None,
        description: Optional[str] = None,
        gt: Optional[float] = None,
        ge: Optional[float] = None,
        lt: Optional[float] = None,
        le: Optional[float] = None,
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/params.py" line="305">

---

## Header Class

The `Header` class is a subclass of `Param` and is used for header parameters. It overrides the `in_` attribute to `ParamTypes.header` and adds a new attribute `convert_underscores`.

```python
class Header(Param):
    in_ = ParamTypes.header

    def __init__(
        self,
        default: Any = Undefined,
        *,
        default_factory: Union[Callable[[], Any], None] = _Unset,
        annotation: Optional[Any] = None,
        alias: Optional[str] = None,
        alias_priority: Union[int, None] = _Unset,
        # TODO: update when deprecating Pydantic v1, import these types
        # validation_alias: str | AliasPath | AliasChoices | None
        validation_alias: Union[str, None] = None,
        serialization_alias: Union[str, None] = None,
        convert_underscores: bool = True,
        title: Optional[str] = None,
        description: Optional[str] = None,
        gt: Optional[float] = None,
        ge: Optional[float] = None,
        lt: Optional[float] = None,
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/params.py" line="391">

---

## Cookie Class

The `Cookie` class is a subclass of `Param` and is used for cookie parameters. It overrides the `in_` attribute to `ParamTypes.cookie`.

```python
class Cookie(Param):
    in_ = ParamTypes.cookie

    def __init__(
        self,
        default: Any = Undefined,
        *,
        default_factory: Union[Callable[[], Any], None] = _Unset,
        annotation: Optional[Any] = None,
        alias: Optional[str] = None,
        alias_priority: Union[int, None] = _Unset,
        # TODO: update when deprecating Pydantic v1, import these types
        # validation_alias: str | AliasPath | AliasChoices | None
        validation_alias: Union[str, None] = None,
        serialization_alias: Union[str, None] = None,
        title: Optional[str] = None,
        description: Optional[str] = None,
        gt: Optional[float] = None,
        ge: Optional[float] = None,
        lt: Optional[float] = None,
        le: Optional[float] = None,
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
