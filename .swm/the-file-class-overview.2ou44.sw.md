---
title: The File Class Overview
---
This document will cover the `File` class in the `fastapi/params.py` file. We'll cover:

1. What the `File` class is and what it is used for.
2. The variables and functions defined in the `File` class.
3. An example of how to use the `File` class.

```mermaid
graph TD;
 Body --> Form --> File:::currentBaseStyle
File --> EnFile

 classDef currentBaseStyle color:#000000,fill:#7CB9F4
```

# What is the File class

The `File` class in `fastapi/params.py` is a subclass of the `Form` class. It is used to handle file uploads in FastAPI. The `File` class is designed to work with multipart/form-data media type, which is the standard for file uploads.

<SwmSnippet path="/fastapi/params.py" line="677">

---

# Variables and functions

The `__init__` function is the constructor of the `File` class. It takes several parameters such as `default`, `default_factory`, `annotation`, `media_type`, `alias`, `alias_priority`, `validation_alias`, `serialization_alias`, `title`, `description`, `gt`, `ge`, `lt`, `le`, `min_length`, `max_length`, `pattern`, `regex`, `discriminator`, `strict`, `multiple_of`, `allow_inf_nan`, `max_digits`, `decimal_places`, `examples`, `example`, `openapi_examples`, `deprecated`, `include_in_schema`, `json_schema_extra`, and `extra`. These parameters are used to configure the `File` instance.

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

# Usage example

Unfortunately, there are no direct usages of the `File` class in the provided context. However, in a typical FastAPI application, the `File` class can be used in a route function to accept file uploads. For example, `def upload_file(file: UploadFile = File(...)): ...`

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="class"><sup>Powered by [Swimm](/)</sup></SwmMeta>
