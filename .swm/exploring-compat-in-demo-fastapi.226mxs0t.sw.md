---
title: Exploring Compat in DEMO-fastapi
---
Compat in the DEMO-fastapi repository refers to a module that provides compatibility support for different versions of the Pydantic library. It contains a series of functions, classes, and variables that help in maintaining compatibility across different versions of Pydantic. For instance, it includes a function `get_definitions` that generates definitions for a list of model fields, and a function `validate` that validates a given value against a set of rules. It also includes a class `BaseConfig` and a variable `Validator` among others. The Compat module plays a crucial role in ensuring that the DEMO-fastapi application can work seamlessly with different versions of Pydantic.

<SwmSnippet path="/fastapi/_compat.py" line="26">

---

# Pydantic Version

The 'PYDANTIC_VERSION' constant is used to store the version of the Pydantic library that is currently being used. This is used to determine which version-specific code to execute.

```python

```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/_compat.py" line="210">

---

# get_definitions Function

The 'get_definitions' function is used to generate definitions for a list of model fields. It takes a list of fields, a schema generator, a model name map, and a flag indicating whether to separate input and output schemas. It returns a tuple containing a field mapping and a dictionary of definitions.

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

The 'BaseConfig' class is a placeholder class that is used as a base class for configuration classes. It does not contain any functionality itself.

```python
    class BaseConfig:
        pass
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/_compat.py" line="118">

---

# validate Function

The 'validate' function is used to validate a given value against a set of rules. It takes a value, a dictionary of values, and a location. It returns a tuple containing the validated value and a list of errors, if any.

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

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
