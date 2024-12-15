
# MASIL XML Specification

Version: 1.0  
Namespace: `http://masil.org/schema/v1`  

This document describes the structure and usage of the MASIL XML Schema and related XML files.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Namespace and Target](#namespace-and-target)
3. [Root Element: `<masil>`](#root-element-masil)
   - [Attributes](#attributes)
4. [Schema Elements](#schema-elements)
   - [`<masil-ai>`](#1-masil-ai)
   - [`<masil-data>`](#2-masil-data)
   - [`<masil-web>`](#3-masil-web)
5. [Complex Types](#complex-types)
   - [`markdownType`](#markdowntype)
   - [`styleType`](#styletype)
   - [`scriptType`](#scripttype)
6. [Example MASIL XML Document](#example-masil-xml-document)
7. [Validation](#validation)

---

## Introduction

MASIL (**M**inder **A**I **S**tructured **I**nteractive **L**anguage) is an open-standard structured language designed for AI workflows. This specification provides a detailed description of the MASIL XML Schema and its components.

MASIL facilitates **"Super Prompts"** and structured AI workflows by enabling:

- **Input Validation:** Define precise data and instructions for the AI.
- **Output Formatting:** Specify structured responses.
- **Data Manipulation:** Automate transformations with ease.

---

## Namespace and Target

- **Namespace:** `http://masil.org/schema/v1`  
- **Target Namespace:** `http://masil.org/schema/v1`  

---

## Root Element: `<masil>`

The root element of any MASIL XML file is `<masil>`. It acts as the container for all MASIL components.

```xml
<masil version="1.0" masil-strict="true" xmlns="http://masil.org/schema/v1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    ...
</masil>
```

### Attributes:

- **`version`** (required): Specifies the schema version.  
  Example: `"1.0"`

- **`masil-strict`** (required): Enables or disables strict validation.  
  Example: `true`

- **`xmlns`**: Fixed to `http://masil.org/schema/v1`

- **`xmlns:xsi`**: Fixed to `http://www.w3.org/2001/XMLSchema-instance`

- **`xsi:schemaLocation`** (required): Points to the MASIL schema file location.

---

## Schema Elements

### 1. `<masil-ai>`

Contains AI-related instructions and configurations.

**Attributes:** None

**Example:**

```xml
<masil-ai>
    <instructions>Analyze the provided data and return insights.</instructions>
</masil-ai>
```

---

### 2. `<masil-data>`

Contains structured data or configuration information.

**Attributes:**

- **`name`** (required): Name of the data set.  
  Example: `"config"`

- **`type`** (optional): Specifies the data type.  
  Example: `"json"`

**Example:**

```xml
<masil-data name="config" type="json">
    {"setting": "value"}
</masil-data>
```

---

### 3. `<masil-web>`

Contains web-related configurations, including styles and scripts.

**Attributes:** None

**Example:**

```xml
<masil-web>
    <style name="theme">body { font-family: sans-serif; }</style>
    <script name="customLogic">console.log("MASIL initialized!");</script>
</masil-web>
```

---

## Complex Types

### `<markdownType>`

Defines the structure of Markdown content in MASIL files.

**Attributes:**

- **`name`** (required): The name of the Markdown block.  
  Example: `"instructions"`

---

### `<styleType>`

Defines the structure of style configurations.

**Attributes:**

- **`name`** (required): The name of the style block.  
  Example: `"theme"`

---

### `<scriptType>`

Defines the structure of script configurations.

**Attributes:**

- **`name`** (required): The name of the script block.  
  Example: `"customLogic"`

---

## Example MASIL XML Document

Below is a full example of a MASIL XML document:

```xml
<masil version="1.0" masil-strict="true" xmlns="http://masil.org/schema/v1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://masil.org/schema/v1 masil.xsd">
    <masil-ai>
        <instructions>Analyze the provided data and return insights.</instructions>
    </masil-ai>
    <masil-data name="config" type="json">
        {"setting": "value"}
    </masil-data>
    <masil-web>
        <style name="theme">body { font-family: sans-serif; }</style>
        <script name="customLogic">console.log("MASIL initialized!");</script>
    </masil-web>
</masil>
```

---

## Validation

To validate MASIL XML files, use the MASIL XSD Schema.

### Download the Schema

[Download MASIL XSD Schema](masil.xsd)

### Validation Command

Use the following command to validate XML files:

```bash
xmllint --schema masil.xsd example.xml --noout
```

---
