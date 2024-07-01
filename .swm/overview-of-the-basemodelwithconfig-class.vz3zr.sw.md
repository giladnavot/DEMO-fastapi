---
title: Overview of the BaseModelWithConfig Class
---
This document will cover the following topics related to the `BaseModelWithConfig` class:

1. What is `BaseModelWithConfig`.
2. Variables and functions in `BaseModelWithConfig`.
3. Usage example of `BaseModelWithConfig`.

```mermaid
graph TD;
  BaseModelWithConfig:::currentBaseStyle
BaseModelWithConfig --> ParameterBase
ParameterBase --> Header
ParameterBase --> Parameter
BaseModelWithConfig --> Response
Response --> CustomORJSONResponse
BaseModelWithConfig --> OAuthFlow
OAuthFlow --> OAuthFlowImplicit
OAuthFlow --> 1[...]
BaseModelWithConfig --> 2[...]

 classDef currentBaseStyle color:#000000,fill:#7CB9F4
```

# What is BaseModelWithConfig

`BaseModelWithConfig` is a class in the `fastapi/openapi/models.py` file. It extends the `BaseModel` class from the `pydantic` library. The purpose of this class is to provide a base model with a specific configuration. This configuration allows extra fields to be included in the model, which are not defined in the model fields, hence providing flexibility in the data that can be included in the model.

<SwmSnippet path="/fastapi/openapi/models.py" line="58">

---

# Variables and functions

`BaseModelWithConfig` has a nested class `Config` which has a single variable `extra`. This variable is set to `allow`, which means that when creating instances of the model, extra fields not defined in the model are allowed.

```python
class BaseModelWithConfig(BaseModel):
    if PYDANTIC_V2:
        model_config = {"extra": "allow"}

    else:

        class Config:
            extra = "allow"
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/openapi/models.py" line="68">

---

# Usage example

`BaseModelWithConfig` is used as a base class for other classes in the `fastapi/openapi/models.py` file. For example, the `Contact` class extends `BaseModelWithConfig`, inheriting its configuration. This means that instances of `Contact` can include extra fields not defined in the `Contact` class.

```python
class Contact(BaseModelWithConfig):
    name: Optional[str] = None
    url: Optional[AnyUrl] = None
    email: Optional[EmailStr] = None
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="class"><sup>Powered by [Swimm](/)</sup></SwmMeta>
