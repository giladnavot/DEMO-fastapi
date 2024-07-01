---
title: ItemBase Class Overview
---
This document will cover the `ItemBase` class from the `schemas.py` file. We'll cover:

1. What is `ItemBase`
2. Variables and functions in `ItemBase`
3. An example of how to use `ItemBase` in `ItemCreate`.

```mermaid
graph TD;
  ItemBase:::currentBaseStyle
ItemBase --> Item
ItemBase --> ItemCreate

 classDef currentBaseStyle color:#000000,fill:#7CB9F4
```

# What is ItemBase

`ItemBase` is a class that serves as a base model for items in the application. It is defined using the Pydantic library's `BaseModel` class, which provides a way to validate data. `ItemBase` is used as a parent class for other classes in the application that need to inherit its properties.

<SwmSnippet path="/docs_src/sql_databases/sql_app_py39/schemas.py" line="7">

---

# Variables in ItemBase

The `title` variable is a string that holds the title of the item.

```python
    title: str
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/sql_databases/sql_app_py39/schemas.py" line="8">

---

The `description` variable is a string that holds the description of the item. It can also be `None` if no description is provided.

```python
    description: Union[str, None] = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/sql_databases/sql_app_py39/schemas.py" line="11">

---

# Usage example

`ItemCreate` is a class that inherits from `ItemBase`. It doesn't add any new properties or methods, meaning it has the same structure as `ItemBase`.

```python
class ItemCreate(ItemBase):
    pass
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="general-class"><sup>Powered by [Swimm](/)</sup></SwmMeta>
