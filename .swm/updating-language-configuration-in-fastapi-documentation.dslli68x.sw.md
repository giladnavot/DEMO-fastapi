---
title: Updating Language Configuration in FastAPI Documentation
---
This document will cover the process of updating the language configuration in the FastAPI documentation. The steps include:

1. Invoking the `new_lang` function
2. Updating the languages with `update_languages`
3. Updating the configuration with `update_config`
4. Getting the updated configuration content with `get_updated_config_content`
5. Using the `Path` function from FastAPI's param_functions.

```mermaid
graph TD;
  new_lang:::mainFlowStyle --> update_languages
  update_languages:::mainFlowStyle --> update_config
  update_config:::mainFlowStyle --> get_updated_config_content
  get_updated_config_content:::mainFlowStyle --> Path
  Path:::mainFlowStyle --> ...

 classDef mainFlowStyle color:#000000,fill:#7CB9F4
  classDef rootsStyle color:#000000,fill:#00FFF4
```

<SwmSnippet path="/scripts/docs.py" line="216">

---

# Invoking the `new_lang` function

The process starts with the `new_lang` function, which calls the `update_languages` function. This function is responsible for updating the `mkdocs.yml` file Languages section including all the available languages.

```python
def update_languages() -> None:
    """
    Update the mkdocs.yml file Languages section including all the available languages.
    """
    update_config()
```

---

</SwmSnippet>

<SwmSnippet path="/scripts/docs.py" line="300">

---

# Updating the languages with `update_languages`

The `update_languages` function calls the `update_config` function. This function updates the configuration of the documentation by getting the updated configuration content.

```python
def update_config() -> None:
    config = get_updated_config_content()
    en_config_path.write_text(
        yaml.dump(config, sort_keys=False, width=200, allow_unicode=True),
        encoding="utf-8",
    )
```

---

</SwmSnippet>

<SwmSnippet path="/scripts/docs.py" line="269">

---

# Updating the configuration with `update_config`

The `update_config` function calls the `get_updated_config_content` function. This function retrieves the current configuration, updates it with the new languages, and returns the updated configuration.

```python
def get_updated_config_content() -> Dict[str, Any]:
    config = get_en_config()
    languages = [{"en": "/"}]
    new_alternate: List[Dict[str, str]] = []
    # Language names sourced from https://quickref.me/iso-639-1
    # Contributors may wish to update or change these, e.g. to fix capitalization.
    language_names_path = Path(__file__).parent / "../docs/language_names.yml"
    local_language_names: Dict[str, str] = mkdocs.utils.yaml_load(
        language_names_path.read_text(encoding="utf-8")
    )
    for lang_path in get_lang_paths():
        if lang_path.name in {"en", "em"} or not lang_path.is_dir():
            continue
        code = lang_path.name
        languages.append({code: f"/{code}/"})
    for lang_dict in languages:
        code = list(lang_dict.keys())[0]
        url = lang_dict[code]
        if code not in local_language_names:
            print(
                f"Missing language name for: {code}, "
```

---

</SwmSnippet>

<SwmSnippet path="/fastapi/param_functions.py" line="11">

---

# Getting the updated configuration content with `get_updated_config_content`

The `get_updated_config_content` function uses the `Path` function from FastAPI's param_functions. This function is used to handle file paths in a platform-independent way.

```python
def Path(  # noqa: N802
    default: Annotated[
        Any,
        Doc(
            """
            Default value if the parameter field is not set.

            This doesn't affect `Path` parameters as the value is always required.
            The parameter is available only for compatibility.
            """
        ),
    ] = ...,
    *,
    default_factory: Annotated[
        Union[Callable[[], Any], None],
        Doc(
            """
            A callable to generate the default value.

            This doesn't affect `Path` parameters as the value is always required.
            The parameter is available only for compatibility.
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBREVNTy1mYXN0YXBpJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="DEMO-fastapi" doc-type="flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>
