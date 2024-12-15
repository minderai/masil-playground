# MASIL Specification

**Markup Language for AI System Integration (MASIL) v1.0**

## Overview

MASIL (Markup Language for AI System Integration) is an XML-based markup language designed to facilitate structured interactions between AI systems, web interfaces, and data components. It provides a standardized way to define AI behaviors, manage data, and handle web presentation layers while maintaining clear separation of concerns.

## Schema

MASIL documents must conform to the XML Schema Definition (XSD) located at `http://masil.org/schema/v1`. All MASIL documents must declare the following namespaces and schema location:

```xml
xmlns="http://masil.org/schema/v1"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://masil.org/schema/v1 masil.xsd"
```

## Document Structure

A MASIL document must contain components in the following strict order:

1. XML Comments (optional, unlimited)
2. `<masil-configuration>` (optional)
3. `<masil-ai>` (required, exactly one)
4. `<masil-data>` (optional, unlimited)
5. `<masil-web>` (optional, maximum one)

### Root Element Requirements

The root element must be `<masil>` with the following required attributes:

- `version`: Document version (e.g., "1.0")
- `masil-strict`: Boolean flag indicating strict mode enforcement
- `xmlns`: Must be "http://masil.org/schema/v1"
- `xmlns:xsi`: Must be "http://www.w3.org/2001/XMLSchema-instance"
- `xsi:schemaLocation`: Must specify schema location

Example:

```xml
<masil version="1.0"
      masil-strict="true"
      xmlns="http://masil.org/schema/v1"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://masil.org/schema/v1 masil.xsd">
    <!-- Content -->
</masil>
```

## Core Components

### 1. AI Component (`<masil-ai>`)

The required AI component can contain:

- Any number of `<masil-data>` elements
- Any other elements (processed by AI)
- Mixed content (text and elements)

Example:

```xml
<masil-ai>
    <masil-data name="vet-info">
        <veterinarian>
            <!-- AI-specific data -->
        </veterinarian>
    </masil-data>
    <!-- Other AI-processed content -->
</masil-ai>
```

### 2. Data Component (`<masil-data>`)

Data components can appear:

- Inside `<masil-ai>`
- At the root level after `<masil-ai>`
- Inside `<masil-web>`

Required attributes:

- `name`: Unique identifier for the data block

Optional attributes:

- `type`: Data format specification (e.g., "json", "csv")

Example:

```xml
<masil-data name="dogs" type="csv">
<![CDATA[
Name,Age,Breed
Max,5,Labrador
]]>
</masil-data>
```

### 3. Web Component (`<masil-web>`)

The optional web component can contain:

- `<masil-data>` elements
- `<markdown>` elements
- `<style>` elements
- `<script>` elements

Each child element requires a `name` attribute.

Example:

```xml
<masil-web>
    <masil-data name="ui-config" type="json">
        <![CDATA[
        {
            "theme": "light"
        }
        ]]>
    </masil-data>
    <markdown name="header">
        <![CDATA[
        # Welcome
        ]]>
    </markdown>
    <style name="custom">
        <![CDATA[
        /* CSS rules */
        ]]>
    </style>
</masil-web>
```

## Processing Model

1. Schema Validation

   - Document structure validation
   - Required attributes verification
   - Component order enforcement

2. AI Processing

   - `<masil-ai>` content processed first
   - Access to all `<masil-data>` elements
   - Placeholder substitution

3. Web Processing
   - `<masil-web>` content processed last
   - Browser-side rendering
   - Style and script application

## Special Features

### Placeholders

Placeholder definitions must appear in XML comments:

```xml
<!--
<placeholders>
  title: Example Title
  version: 1.0
</placeholders>
-->
```

### AI Guidance

AI instructions must be placed in XML comments:

```xml
<!--
# AI to follow these instructions:
ai-guidance
- Process data in CSV format
- Respond in markdown
-->
```

## Error Handling

The schema enforces:

1. Component order
2. Required attributes
3. Element nesting rules
4. Namespace requirements

Implementations must:

1. Validate before processing
2. Handle CDATA appropriately
3. Sanitize data inputs
4. Provide clear error messages

## Best Practices

1. Use CDATA for all embedded content
2. Keep AI, data, and web components separate
3. Validate against the schema before processing
4. Use meaningful names for data blocks
5. Include clear AI guidance
6. Document all placeholder usage

## Version History

- 1.0: Initial release
  - XML Schema definition
  - Core component structure
  - Processing model
  - Validation rules

Enter `/help` to see what AI can do.
