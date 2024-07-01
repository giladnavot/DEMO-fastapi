---
title: Understanding Params in FastAPI
---
Params in FastAPI are used to define parameters that can be passed to an endpoint. They are used to extract and validate data from different parts of a request such as the path, query, headers, and cookies. The `Param` class in FastAPI provides a way to define these parameters and their characteristics such as default values, validation rules, and serialization behavior.

There are different types of Params in FastAPI, each represented by a class that inherits from the `Param` class. These include `Query`, `Path`, `Header`, `Cookie`, `Form`, and `File`. Each of these classes represents a different type of parameter and has its own specific behavior and validation rules.

For example, the `Query` class is used to define parameters that are passed in the query string of the URL, while the `Path` class is used for parameters that are part of the URL path. The `Header` and `Cookie` classes are used for parameters that are passed in the headers and cookies of the request respectively. The `Form` and `File` classes are used for parameters that are part of a form submission.

Each Param class has an `in_` attribute that specifies where the parameter is expected to be in the request. This attribute is set to one of the values of the `ParamTypes` enum, which includes `query`, `header`, `path`, and `cookie`.

The `Depends` class is used to express dependencies between parameters. This can be used to ensure that certain parameters are only processed if other parameters have certain values.

<SwmSnippet path="/fastapi/params.py" line="21">

---

## Param Class

The `Param` class is the base class for all types of parameters. It inherits from `FieldInfo` and defines common attributes for all parameters like `default`, `alias`, `title`, `description`, `deprecated`, etc. It also defines the `__init__` method which is used to initialize these attributes.

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

## Query Class

The `Query` class is used to define parameters that are expected in the query string of the request URL. It inherits from the `Param` class and sets the 'in\_' attribute to 'query'.

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

## Path Class

The `Path` class is used to define parameters that are expected in the path of the request URL. It inherits from the `Param` class and sets the 'in\_' attribute to 'path'.

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

## Header Class

The `Header` class is used to define parameters that are expected in the headers of the request. It inherits from the `Param` class and sets the 'in\_' attribute to 'header'.

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

The `Cookie` class is used to define parameters that are expected in the cookies of the request. It inherits from the `Param` class and sets the 'in\_' attribute to 'cookie'.

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

<SwmSnippet path="/fastapi/params.py" line="761">

---

## Depends Class

The `Depends` class is used to define dependencies for your API endpoint. It doesn't inherit from the `Param` class but is still considered a type of parameter. It is used to define complex dependencies for your API endpoint.

```python
class Depends:
    def __init__(
        self, dependency: Optional[Callable[..., Any]] = None, *, use_cache: bool = True
    ):
        self.dependency = dependency
        self.use_cache = use_cache

    def __repr__(self) -> str:
        attr = getattr(self.dependency, "__name__", type(self.dependency).__name__)
```

---

</SwmSnippet>

# Parameter Types

This section covers the different types of parameters that can be used in a FastAPI application.

<SwmSnippet path="/fastapi/params.py" line="135">

---

## Path Parameters

The `Path` class is used to define parameters that are part of the URL path. The constructor of this class takes various arguments such as default value, alias, validation rules, etc.

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

## Query Parameters

The `Query` class is used to define parameters that are passed in the URL query string. The constructor of this class takes various arguments similar to the `Path` class.

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

## Header Parameters

The `Header` class is used to define parameters that are passed in the request header. The constructor of this class takes various arguments similar to the `Path` and `Query` classes.

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

## Cookie Parameters

The `Cookie` class is used to define parameters that are passed in the cookies of the request. The constructor of this class takes various arguments similar to the other parameter classes.

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

<SwmSnippet path="/fastapi/params.py" line="475">

---

## Body Parameters

The `Body` class is used to define parameters that are passed in the body of the request. The constructor of this class takes various arguments similar to the other parameter classes.

```python
class Body(FieldInfo):
    def __init__(
        self,
        default: Any = Undefined,
        *,
        default_factory: Union[Callable[[], Any], None] = _Unset,
        annotation: Optional[Any] = None,
        embed: bool = False,
        media_type: str = "application/json",
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

<SwmSnippet path="/fastapi/params.py" line="592">

---

## Form Parameters

The `Form` class is used to define parameters that are passed in the form data of the request. The constructor of this class takes various arguments similar to the other parameter classes.

```python
class Form(Body):
    def __init__(
        self,
        default: Any = Undefined,
        *,
        default_factory: Union[Callable[[], Any], None] = _Unset,
        annotation: Optional[Any] = None,
        media_type: str = "application/x-www-form-urlencoded",
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
        min_length: Optional[int] = None,
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/params.py" line="677">

---

## File Parameters

The `File` class is used to define parameters that are passed as file uploads in the request. The constructor of this class takes various arguments similar to the other parameter classes.

```python
class File(Form):
    def __init__(
        self,
        default: Any = Undefined,
        *,
        default_factory: Union[Callable[[], Any], None] = _Unset,
        annotation: Optional[Any] = None,
        media_type: str = "multipart/form-data",
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
        min_length: Optional[int] = None,
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/params.py" line="761">

---

## Dependency Parameters

The `Depends` class is used to define dependencies that need to be injected into the path operation function. The constructor of this class takes a dependency function as an argument.

```python
class Depends:
    def __init__(
        self, dependency: Optional[Callable[..., Any]] = None, *, use_cache: bool = True
    ):
        self.dependency = dependency
        self.use_cache = use_cache

    def __repr__(self) -> str:
        attr = getattr(self.dependency, "__name__", type(self.dependency).__name__)
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/params.py" line="774">

---

## Security Parameters

The `Security` class is used to define parameters that are used for security schemes. The constructor of this class takes a dependency function and a list of scopes as arguments.

```python
class Security(Depends):
    def __init__(
        self,
        dependency: Optional[Callable[..., Any]] = None,
        *,
        scopes: Optional[Sequence[str]] = None,
        use_cache: bool = True,
    ):
        super().__init__(dependency=dependency, use_cache=use_cache)
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
