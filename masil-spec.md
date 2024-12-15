# MASIL v1.0

> **M**arkup **L**anguage for **A**I **S**ystem **I**ntegration\*

---

## Overview

MASIL (Markup Language for AI System Integration) is an XML-based markup language designed to facilitate structured interactions between AI systems, web interfaces, and data components. It provides a standardized way to define AI behaviors, manage data, and handle web presentation layers while maintaining clear separation of concerns.

## Schema

**All MASIL documents must** conform to the XML Schema Definition (XSD) located at `http://masil.org/schema/v1` and declare these **required namespaces**:

```xml
xmlns="http://masil.org/schema/v1"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://masil.org/schema/v1 masil.xsd"
```

## Document Structure

A MASIL document **must** contain components in the following **strict order**:

1. XML Comments (optional, unlimited)
2. `<masil-configuration>` (optional)
3. **`<masil-ai>`** (**required**, exactly one)
4. `<masil-data>` (optional, unlimited)
5. `<masil-web>` (optional, maximum one)

> **Important**: The order of components is strictly enforced by the schema and cannot be changed.

### Root Element Requirements

The root element `<masil>` **requires** the following attributes:

- **`version`**: Document version (e.g., "1.0")
- **`masil-strict`**: Boolean flag indicating strict mode enforcement
- **`xmlns`**: Must be "http://masil.org/schema/v1"
- **`xmlns:xsi`**: Must be "http://www.w3.org/2001/XMLSchema-instance"
- **`xsi:schemaLocation`**: Must specify schema location

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

**Required component**. Can contain:

- Any number of `<masil-data>` elements
- `<markdown>` elements
- Any other elements (processed by AI)
- Mixed content (text and elements)

> **Note**: All content within `<masil-ai>` is processed by the AI system.

Example:

```xml
<masil-ai>
    <masil-data name="vet-info">
        <veterinarian>
            <!-- AI-specific data -->
        </veterinarian>
    </masil-data>
    <markdown name="greeting">
        <![CDATA[
        # Welcome to our veterinary service
        ]]>
    </markdown>
</masil-ai>
```

### 2. Data Component (`<masil-data>`)

Can appear in **three locations**:

- Inside `<masil-ai>`
- At the root level after `<masil-ai>`
- Inside `<masil-web>`

**Required** attributes:

- **`name`**: Unique identifier for the data block

_Optional_ attributes:

- `type`: Data format specification (e.g., "json", "csv")

> **Best Practice**: Always wrap data content in CDATA sections

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

Optional component for browser-side presentation. Can contain:

- `<masil-data>` elements
- `<markdown>` elements (for web display)
- `<style>` elements
- `<script>` elements

> **Important**: Each child element **requires** a `name` attribute. Content in this section is processed by the web browser rather than the AI system.

## Processing Model

1. **Schema Validation** (_Required First Step_)

   - Document structure validation
   - Required attributes verification
   - Component order enforcement

2. **AI Processing**

   - `<masil-ai>` content processed first
   - Access to all `<masil-data>` elements
   - Placeholder substitution

3. **Web Processing**
   - `<masil-web>` content processed last
   - Browser-side rendering
   - Style and script application

## Special Features

### Placeholders

**Must** appear in XML comments:

```xml
<!--
<placeholders>
  title: Example Title
  version: 1.0
</placeholders>
-->
```

### AI Guidance

**Must** be placed in XML comments:

```xml
<!--
# AI to follow these instructions:
ai-guidance
- Process data in CSV format
- Respond in markdown
-->
```

## Error Handling

**Schema Enforcement**:

- Component order
- Required attributes
- Element nesting rules
- Namespace requirements

**Implementation Requirements**:

1. **Must** validate before processing
2. **Must** handle CDATA appropriately
3. **Must** sanitize data inputs
4. **Must** provide clear error messages

## Best Practices

1. **Always** use CDATA for embedded content
2. **Maintain** separation between AI, data, and web components
3. **Validate** against schema before processing
4. Use meaningful names for data blocks
5. Include clear AI guidance
6. Document all placeholder usage

> **Security Note**: Always sanitize data inputs and validate content before processing.

## Version History

- **1.0**: Initial release
  - XML Schema definition
  - Core component structure
  - Processing model
  - Validation rules

Enter `/help` to see what AI can do.

## Configuration Options

The optional `<masil-configuration>` element controls system behavior:

**Available Settings**:

- **`show_developer_help`**: Boolean, enables developer guidance
- **`show_user_help`**: Boolean, enables user help features

Example:

```xml
<masil-configuration>
    <show_developer_help>true</show_developer_help>
    <show_user_help>true</show_user_help>
</masil-configuration>
```

## Command Interface

MASIL provides built-in commands for AI interaction:

- **`/report`**: Display markdown report
- **`/explain`**: Show data in tabular form
- **`/update`**: Display CSV data with AI modifications
- **`/validate`**: Validate data accuracy
- **`/fix`**: Correct data based on AI validation
- **`/random`**: Add random records to data
- **`/history`**: Show numbered list of session prompts
- **`/summary`**: Summarize chat session
- **`/help`**: Display available commands

## Data Types

The `type` attribute in `<masil-data>` supports:

- **`csv`**: Comma-separated values

  ```xml
  <masil-data name="example" type="csv">
  <![CDATA[
  header1,header2
  value1,value2
  ]]>
  </masil-data>
  ```

- **`json`**: JSON format
  ```xml
  <masil-data name="config" type="json">
  <![CDATA[
  {
    "setting": "value"
  }
  ]]>
  </masil-data>
  ```
