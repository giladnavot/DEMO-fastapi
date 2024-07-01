---
title: Field-Type Specific Validation in FastAPI
---
This document will cover the process of validation for different types of fields in the DEMO-fastapi repository. We'll cover:

1. How file fields are validated
2. How request body fields are validated
3. How validation errors are handled.

<SwmSnippet path="/fastapi/dependencies/utils.py" line="82">

---

# File Field Validation

The `check_file_field` function is used to validate file fields. It checks if the field is of type `Form` and if the `multipart` library is correctly installed. If not, it raises an error.

```python
def check_file_field(field: ModelField) -> None:
    field_info = field.field_info
    if isinstance(field_info, params.Form):
        try:
            # __version__ is available in both multiparts, and can be mocked
            from multipart import __version__  # type: ignore

            assert __version__
            try:
                # parse_options_header is only available in the right multipart
                from multipart.multipart import parse_options_header  # type: ignore

                assert parse_options_header
            except ImportError:
                logger.error(multipart_incorrect_install_error)
                raise RuntimeError(multipart_incorrect_install_error) from None
        except ImportError:
            logger.error(multipart_not_installed_error)
            raise RuntimeError(multipart_not_installed_error) from None
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/dependencies/utils.py" line="687">

---

# Request Body Field Validation

The `request_body_to_args` function is used to validate request body fields. It checks if the field is required and if it is present in the received body. If the field is missing, it appends an error to the errors list. If the field is of type `File` and is a bytes field, it reads the file content.

```python
async def request_body_to_args(
    required_params: List[ModelField],
    received_body: Optional[Union[Dict[str, Any], FormData]],
) -> Tuple[Dict[str, Any], List[Dict[str, Any]]]:
    values = {}
    errors: List[Dict[str, Any]] = []
    if required_params:
        field = required_params[0]
        field_info = field.field_info
        embed = getattr(field_info, "embed", None)
        field_alias_omitted = len(required_params) == 1 and not embed
        if field_alias_omitted:
            received_body = {field.alias: received_body}

        for field in required_params:
            loc: Tuple[str, ...]
            if field_alias_omitted:
                loc = ("body",)
            else:
                loc = ("body", field.alias)

```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/openapi/utils.py" line="36">

---

# Validation Error Handling

The `validation_error_definition` constant defines the structure of a validation error. It includes the location of the error (`loc`), the error message (`msg`), and the error type (`type`).

```python
validation_error_definition = {
    "title": "ValidationError",
    "type": "object",
    "properties": {
        "loc": {
            "title": "Location",
            "type": "array",
            "items": {"anyOf": [{"type": "string"}, {"type": "integer"}]},
        },
        "msg": {"title": "Message", "type": "string"},
        "type": {"title": "Error Type", "type": "string"},
    },
    "required": ["loc", "msg", "type"],
}
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="follow-up"><sup>Powered by [Swimm](/)</sup></SwmMeta>
