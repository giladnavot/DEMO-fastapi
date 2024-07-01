---
title: Handling Changes in Pydantic Model Fields
---
This document will cover the implications of changing a field in a Pydantic model within the DEMO-fastapi repository. We'll cover:

1. What is a Pydantic model
2. How fields are defined in a Pydantic model
3. What happens when a field in the Pydantic model changes

# What is a Pydantic model

A Pydantic model is a class that inherits from `pydantic.BaseModel`. It is used for data validation by defining the data shape with Python type annotations. In the DEMO-fastapi repository, Pydantic models are used to define request and response models for the FastAPI routes.

<SwmSnippet path="/docs_src/body_fields/tutorial001.py" line="4">

---

# How fields are defined in a Pydantic model

Fields in a Pydantic model are defined as class attributes. The `Field` function from the `pydantic` module is used to provide extra information about the field, such as a description or alias.

```python
from pydantic import BaseModel, Field
```

---

</SwmSnippet>

# What happens when a field in the Pydantic model changes

When a field in a Pydantic model changes, it affects the data validation and serialization/deserialization processes. If a field is added or removed, the data shape changes and the validation rules are updated accordingly. If the type of a field changes, the validation and serialization/deserialization processes will follow the new type's rules. If the extra information provided by the `Field` function changes, it will affect the OpenAPI schema and the interactive API documentation.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="follow-up"><sup>Powered by [Swimm](/)</sup></SwmMeta>
