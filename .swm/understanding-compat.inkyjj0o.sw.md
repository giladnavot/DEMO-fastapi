---
title: Understanding Compat
---
Compat in the DEMO-fastapi repository refers to the compatibility layer between different versions of the Pydantic library. It provides a unified interface to interact with Pydantic's features, regardless of the version being used. This is achieved by checking the Pydantic version and importing the appropriate modules and functions accordingly. It also includes utility functions and classes that help in handling Pydantic models, fields, and validation errors.

<SwmSnippet path="/fastapi/_compat.py" line="26">

---

# Global Constants

The 'compat' module defines several global constants, such as 'PYDANTIC_VERSION' and 'sequence_types'. These constants are used throughout the codebase to handle different versions of Pydantic and to map different types of sequences to their corresponding Python types.

```python

# Reassign variable to make it reexported for mypy
PYDANTIC_VERSION = P_VERSION
PYDANTIC_V2 = PYDANTIC_VERSION.startswith("2.")


sequence_annotation_to_type = {
    Sequence: list,
    List: list,
    list: list,
    Tuple: tuple,
    tuple: tuple,
    Set: set,
    set: set,
    FrozenSet: frozenset,
    frozenset: frozenset,
    Deque: deque,
    deque: deque,
}

sequence_types = tuple(sequence_annotation_to_type.keys())
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/_compat.py" line="210">

---

# get_definitions Function

The 'get_definitions' function is used to generate definitions for a list of model fields. It takes several parameters, including a list of fields, a schema generator, and a model name map, and returns a tuple containing a field mapping and a dictionary of definitions.

```python
    def get_definitions(
        *,
        fields: List[ModelField],
        schema_generator: GenerateJsonSchema,
        model_name_map: ModelNameMap,
        separate_input_output_schemas: bool = True,
    ) -> Tuple[
        Dict[
            Tuple[ModelField, Literal["validation", "serialization"]], JsonSchemaValue
        ],
        Dict[str, Dict[str, Any]],
    ]:
        override_mode: Union[Literal["validation"], None] = (
            None if separate_input_output_schemas else "validation"
        )
        inputs = [
            (field, override_mode or field.mode, field._type_adapter.core_schema)
            for field in fields
        ]
        field_mapping, definitions = schema_generator.generate_definitions(
            inputs=inputs
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/_compat.py" line="79">

---

# BaseConfig Class

The 'BaseConfig' class is a simple class that doesn't define any methods or attributes. It is used as a base class for Pydantic models in the codebase.

```python
    class BaseConfig:
        pass
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/_compat.py" line="118">

---

# validate Function

The 'validate' function is used to validate a value against a model field. It takes several parameters, including the value to validate and a dictionary of values, and returns a tuple containing the validated value and a list of validation errors, if any.

```python
        def validate(
            self,
            value: Any,
            values: Dict[str, Any] = {},  # noqa: B006
            *,
            loc: Tuple[Union[int, str], ...] = (),
        ) -> Tuple[Any, Union[List[Dict[str, Any]], None]]:
            try:
                return (
                    self._type_adapter.validate_python(value, from_attributes=True),
                    None,
                )
            except ValidationError as exc:
                return None, _regenerate_error_with_loc(
                    errors=exc.errors(include_url=False), loc_prefix=loc
                )
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/_compat.py" line="517">

---

# \_regenerate_error_with_loc Function

The '\_regenerate_error_with_loc' function is a helper function used by the 'validate' function to regenerate validation errors with a location prefix. It takes a sequence of errors and a location prefix as parameters, and returns a list of updated errors.

```python
def _regenerate_error_with_loc(
    *, errors: Sequence[Any], loc_prefix: Tuple[Union[str, int], ...]
) -> List[Dict[str, Any]]:
    updated_loc_errors: List[Any] = [
        {**err, "loc": loc_prefix + err.get("loc", ())}
        for err in _normalize_errors(errors)
    ]

    return updated_loc_errors
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
