---
title: Exploring OpenAPI in FastAPI
---
OpenAPI is a specification used to define APIs. In the DEMO-fastapi repository, OpenAPI is used to generate documentation for the API endpoints. This is done using the FastAPI framework's built-in support for OpenAPI. The `get_openapi` function in `fastapi/openapi/utils.py` is responsible for generating the OpenAPI specification. This function takes information about the API (such as its title, version, and the routes it contains) and returns a dictionary representing the API in the OpenAPI format. This dictionary can then be serialized to JSON or YAML, and used to generate documentation or client SDKs.

<SwmSnippet path="/fastapi/openapi/utils.py" line="438">

---

# OpenAPI Specification Generation

The `get_openapi` function is used to generate the OpenAPI specification. It takes in the API title, version, and other optional parameters, and returns a dictionary representing the OpenAPI specification. This function is called when the '/openapi.json' endpoint is accessed.

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

<SwmSnippet path="/fastapi/openapi/utils.py" line="215">

---

# OpenAPI Path Generation

The `get_openapi_path` function is used to generate the OpenAPI paths for each API route. It takes in the route, operation IDs, and other parameters, and returns a dictionary representing the OpenAPI paths. This function is called for each route when generating the OpenAPI specification.

```python
def get_openapi_path(
    *,
    route: routing.APIRoute,
    operation_ids: Set[str],
    schema_generator: GenerateJsonSchema,
    model_name_map: ModelNameMap,
    field_mapping: Dict[
        Tuple[ModelField, Literal["validation", "serialization"]], JsonSchemaValue
    ],
    separate_input_output_schemas: bool = True,
) -> Tuple[Dict[str, Any], Dict[str, Any], Dict[str, Any]]:
    path = {}
    security_schemes: Dict[str, Any] = {}
    definitions: Dict[str, Any] = {}
    assert route.methods is not None, "Methods must be a list"
    if isinstance(route.response_class, DefaultPlaceholder):
        current_response_class: Type[Response] = route.response_class.value
    else:
        current_response_class = route.response_class
    assert current_response_class, "A response class is needed to generate OpenAPI"
    route_response_media_type: Optional[str] = current_response_class.media_type
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/openapi/utils.py" line="90">

---

# OpenAPI Parameter Generation

The `get_openapi_operation_parameters` function is used to generate the OpenAPI parameters for each API route. It takes in the route parameters and other parameters, and returns a list of dictionaries representing the OpenAPI parameters. This function is called for each route when generating the OpenAPI paths.

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

<SwmSnippet path="/fastapi/openapi/utils.py" line="131">

---

# OpenAPI Request Body Generation

The `get_openapi_operation_request_body` function is used to generate the OpenAPI request body for each API route. It takes in the body field and other parameters, and returns a dictionary representing the OpenAPI request body. This function is called for each route when generating the OpenAPI paths.

```python
def get_openapi_operation_request_body(
    *,
    body_field: Optional[ModelField],
    schema_generator: GenerateJsonSchema,
    model_name_map: ModelNameMap,
    field_mapping: Dict[
        Tuple[ModelField, Literal["validation", "serialization"]], JsonSchemaValue
    ],
    separate_input_output_schemas: bool = True,
) -> Optional[Dict[str, Any]]:
    if not body_field:
        return None
    assert isinstance(body_field, ModelField)
    body_schema = get_schema_from_model_field(
        field=body_field,
        schema_generator=schema_generator,
        model_name_map=model_name_map,
        field_mapping=field_mapping,
        separate_input_output_schemas=separate_input_output_schemas,
    )
    field_info = cast(Body, body_field.field_info)
```

---

</SwmSnippet>

# OpenAPI Functions

This section will cover the main OpenAPI functions used in the DEMO-fastapi repository.

<SwmSnippet path="/fastapi/openapi/utils.py" line="73">

---

## get_openapi_security_definitions

The `get_openapi_security_definitions` function is used to generate security definitions for the OpenAPI schema. It takes a `Dependant` object as input and returns a tuple containing security definitions and operation security.

```python
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
        security_name = security_requirement.security_scheme.scheme_name
        security_definitions[security_name] = security_definition
        operation_security.append({security_name: security_requirement.scopes})
    return security_definitions, operation_security
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/openapi/utils.py" line="90">

---

## get_openapi_operation_parameters

The `get_openapi_operation_parameters` function is used to generate OpenAPI operation parameters. It takes several parameters including a list of all route parameters, a schema generator, a model name map, and a field mapping. It returns a list of parameters for the OpenAPI operation.

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

<SwmSnippet path="/fastapi/openapi/utils.py" line="131">

---

## get_openapi_operation_request_body

The `get_openapi_operation_request_body` function is used to generate the OpenAPI operation request body. It takes several parameters including an optional body field, a schema generator, a model name map, and a field mapping. It returns an optional dictionary representing the OpenAPI operation request body.

```python
def get_openapi_operation_request_body(
    *,
    body_field: Optional[ModelField],
    schema_generator: GenerateJsonSchema,
    model_name_map: ModelNameMap,
    field_mapping: Dict[
        Tuple[ModelField, Literal["validation", "serialization"]], JsonSchemaValue
    ],
    separate_input_output_schemas: bool = True,
) -> Optional[Dict[str, Any]]:
    if not body_field:
        return None
    assert isinstance(body_field, ModelField)
    body_schema = get_schema_from_model_field(
        field=body_field,
        schema_generator=schema_generator,
        model_name_map=model_name_map,
        field_mapping=field_mapping,
        separate_input_output_schemas=separate_input_output_schemas,
    )
    field_info = cast(Body, body_field.field_info)
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
