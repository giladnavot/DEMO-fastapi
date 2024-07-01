---
title: Overview of the BaseItem Class
---
This document will cover the following aspects of the `BaseItem` class:

1. What is `BaseItem`.
2. Variables and functions in `BaseItem`.
3. An example of how to use `BaseItem`.

```mermaid
graph TD;
  BaseItem:::currentBaseStyle
BaseItem --> PlaneItem
BaseItem --> CarItem

 classDef currentBaseStyle color:#000000,fill:#7CB9F4
```

# What is BaseItem

`BaseItem` is a class that serves as a base model for other classes in the application. It is defined using the `BaseModel` class from the `pydantic` library, which is a data validation library used to validate that the data structures (like JSON) match the expected models. `BaseItem` is used to define common attributes for other classes that inherit from it.

<SwmSnippet path="/docs_src/extra_models/tutorial003_py310.py" line="10">

---

# Variables in BaseItem

The variable `description` is a string that is used to store a description of the item.

```python
    description: str
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/extra_models/tutorial003_py310.py" line="11">

---

The variable `type` is a string that is used to store the type of the item.

```python
    type: str
```

---

</SwmSnippet>

<SwmSnippet path="/docs_src/extra_models/tutorial003_py310.py" line="14">

---

# Usage example

`CarItem` is an example of a class that extends `BaseItem`. It inherits the `description` and `type` variables from `BaseItem` and sets the `type` variable to 'car'.

```python
class CarItem(BaseItem):
    type: str = "car"
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="general-class"><sup>Powered by [Swimm](/)</sup></SwmMeta>
