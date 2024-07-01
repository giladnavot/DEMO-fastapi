---
title: ItemBase Class Overview
---
This document will cover the `ItemBase` class in the DEMO-fastapi repository. We'll cover:

1. What is `ItemBase`
2. Variables and functions in `ItemBase`
3. Usage example of `ItemBase`

```mermaid
graph TD;
  ItemBase:::currentBaseStyle
ItemBase --> Item
ItemBase --> ItemCreate

 classDef currentBaseStyle color:#000000,fill:#7CB9F4
```

# What is ItemBase

`ItemBase` is a class defined in the `schemas.py` file of the `sql_databases_peewee` directory. It is a Pydantic model that represents the base schema for an item in the application. It is used as a base class for other item-related classes in the application.

<SwmSnippet path="/docs_src/sql_databases_peewee/sql_app/schemas.py" line="17">

---

# Variables in ItemBase

The `title` variable is a string that represents the title of an item.

```python
    title: str
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/sql_databases_peewee/sql_app/schemas.py" line="18">

---

The `description` variable is an optional string that provides a description of an item. It can be `None` if no description is provided.

```python
    description: Union[str, None] = None
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/sql_databases_peewee/sql_app/schemas.py" line="21">

---

# Usage example

`ItemBase` is used as a base class for `ItemCreate`. `ItemCreate` inherits all the properties of `ItemBase`.

```python
class ItemCreate(ItemBase):
    pass
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="general-class"><sup>Powered by [Swimm](/)</sup></SwmMeta>
