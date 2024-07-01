---
title: API
---
This document will cover the process of using the API in the DEMO-fastapi repository. We'll cover:

1. An overview of what the API offers and some endpoints.
2. Where to find the list of endpoints.
3. Each API documentation tool available in the repo.
4. What this specific API offers and how it is used.

<SwmSnippet path="/fastapi/openapi/utils.py" line="63">

---

# Overview of the API

The `get_openapi_security_definitions` function is used to generate security definitions for the API. It iterates over the security requirements of the API and encodes them into a format that can be used in the OpenAPI schema.

```python
status_code_ranges: Dict[str, str] = {
    "1XX": "Information",
    "2XX": "Success",
    "3XX": "Redirection",
    "4XX": "Client Error",
    "5XX": "Server Error",
    "DEFAULT": "Default Response",
}


def get_openapi_security_definitions(
    flat_dependant: Dependant,
) -> Tuple[Dict[str, Any], List[Dict[str, Any]]]:
    security_definitions = {}
    operation_security = []
    for security_requirement in flat_dependant.security_requirements:
        security_definition = jsonable_encoder(
            security_requirement.security_scheme.model,
            by_alias=True,
            exclude_none=True,
        )
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/openapi/utils.py" line="90">

---

# List of Endpoints

The `get_openapi_operation_parameters` function is used to generate the parameters for each operation in the API. It iterates over all the route parameters and includes them in the schema if they are to be included in the schema.

```python
def get_openapi_operation_parameters(
    *,
    all_route_params: Sequence[ModelField],
    schema_generator: GenerateJsonSchema,
    model_name_map: ModelNameMap,
    field_mapping: Dict[
        Tuple[ModelField, Literal["validation", "serialization"]], JsonSchemaValue
    ],
    separate_input_output_schemas: bool = True,
) -> List[Dict[str, Any]]:
    parameters = []
    for param in all_route_params:
        field_info = param.field_info
        field_info = cast(Param, field_info)
        if not field_info.include_in_schema:
            continue
        param_schema = get_schema_from_model_field(
            field=param,
            schema_generator=schema_generator,
            model_name_map=model_name_map,
            field_mapping=field_mapping,
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/openapi/utils.py" line="438">

---

# API Documentation Tools

The `get_openapi` function is used to generate the OpenAPI schema for the API. This schema is used by documentation tools like Swagger and ReDoc to generate interactive API documentation.

```python
def get_openapi(
    *,
    title: str,
    version: str,
    openapi_version: str = "3.1.0",
    summary: Optional[str] = None,
    description: Optional[str] = None,
    routes: Sequence[BaseRoute],
    webhooks: Optional[Sequence[BaseRoute]] = None,
    tags: Optional[List[Dict[str, Any]]] = None,
    servers: Optional[List[Dict[str, Union[str, Any]]]] = None,
    terms_of_service: Optional[str] = None,
    contact: Optional[Dict[str, Union[str, Any]]] = None,
    license_info: Optional[Dict[str, Union[str, Any]]] = None,
    separate_input_output_schemas: bool = True,
) -> Dict[str, Any]:
    info: Dict[str, Any] = {"title": title, "version": version}
    if summary:
        info["summary"] = summary
    if description:
        info["description"] = description
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/openapi/utils.py" line="36">

---

# API Functionality

The API uses HTTP status codes to indicate the success or failure of a request. These status codes are defined in the `status_code_ranges` dictionary.

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

validation_error_response_definition = {
    "title": "HTTPValidationError",
    "type": "object",
    "properties": {
        "detail": {
            "title": "Detail",
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="api"><sup>Powered by [Swimm](/)</sup></SwmMeta>
