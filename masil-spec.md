# MASIL Specification

**Markup Language for AI System Integration (MASIL) v1.0**

## Overview

MASIL (Markup Language for AI System Integration) is an XML-based markup language designed to facilitate structured interactions between AI systems, web interfaces, and data components. It provides a standardized way to define AI behaviors, manage data, and handle web presentation layers while maintaining clear separation of concerns.

## Schema

MASIL documents must conform to the XML Schema Definition (XSD) located at `http://masil.org/schema/v1`. All MASIL documents must declare the following namespace:

```xml
xmlns="http://masil.org/schema/v1"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://masil.org/schema/v1 masil.xsd"
```

## Document Structure

A MASIL document consists of three main sections:

1. `<masil-ai>`: Contains AI-specific configurations and data
2. `<masil-data>`: Defines data structures and content
3. `<masil-web>`: Contains web presentation components (optional)

### Root Element

The root element must be `<masil>` with the following required attributes:

- `version`: Document version (e.g., "1.0")
- `masil-strict`: Boolean flag indicating strict mode enforcement

Example:

```xml
<masil version="1.0" masil-strict="true">
    <!-- Content -->
</masil>
```

## Core Components

### 1. AI Component (`<masil-ai>`)

The AI component contains configurations and data specifically processed by AI systems. It may include:

- AI behavior definitions
- Role-specific information
- Processing instructions
- AI-specific data structures

Example:

```xml
<masil-ai>
    <masil-data name="ai-config">
        <!-- AI-specific configuration -->
    </masil-data>
</masil-ai>
```

### 2. Data Component (`<masil-data>`)

The data component is used to store and manage structured data. Each data block must have a unique `name` attribute.

Attributes:

- `name` (required): Unique identifier for the data block
- `type` (optional): Data format specification (e.g., "json", "csv")

Example:

```xml
<masil-data name="example-data" type="csv">
<![CDATA[
header1,header2,header3
value1,value2,value3
]]>
</masil-data>
```

### 3. Web Component (`<masil-web>`)

The web component contains presentation-layer elements. It may include:

#### Markdown Blocks

```xml
<markdown name="section-name">
<![CDATA[
# Markdown content
]]>
</markdown>
```

#### Styles

```xml
<style name="custom-styles">
<![CDATA[
/* CSS content */
]]>
</style>
```

## Special Features

### Placeholders

MASIL supports placeholder substitution using the following syntax:

```yaml
<placeholders>
  key: value
</placeholders>
```

Placeholders can be referenced using `[key]` notation throughout the document.

### AI Guidance

AI processing instructions can be included in XML comments using the `ai-guidance` section:

```xml
<!--
# AI to follow these instructions:
ai-guidance
- Instruction 1
- Instruction 2
-->
```

## Data Validation

MASIL documents must validate against the official schema. The schema enforces:

- Required components and their order
- Attribute requirements
- Namespace declarations
- Component nesting rules

## Best Practices

1. Always use CDATA sections for embedded content
2. Maintain clear separation between AI, data, and web components
3. Use meaningful names for data blocks and components
4. Include version information in the root element
5. Validate documents against the official schema

## Security Considerations

1. Sanitize all data inputs
2. Use CDATA sections to prevent XML injection
3. Validate all placeholder substitutions
4. Implement appropriate access controls for AI processing

## Extensions

MASIL can be extended through:

1. Custom data types
2. Additional component definitions
3. Extended schema definitions

## Commands and Interactions

MASIL supports several built-in commands for interacting with the AI:

- `/report`: Display markdown report
- `/explain`: Show data in tabular form
- `/update`: Display CSV data with AI modifications
- `/validate`: Validate data accuracy
- `/fix`: Correct data based on AI validation
- `/random`: Add random records to data
- `/history`: Show numbered list of session prompts
- `/summary`: Summarize chat session
- `/introduction`: Meet the AI persona
- `/help`: Display available commands

## Version History

- 1.0: Initial release
  - Basic component structure
  - AI processing support
  - Web component integration
  - Data management capabilities
  - Command interface implementation

## Implementation Requirements

### Required Components

1. XML Schema validation
2. AI processing engine
3. Placeholder substitution system
4. Command interpreter
5. Data validation system

### Optional Components

1. Web rendering engine
2. Style processor
3. Script handler
4. Extended command modules

## Error Handling

MASIL implementations should:

1. Validate XML structure before processing
2. Provide clear error messages for schema violations
3. Handle missing or malformed data gracefully
4. Log processing errors appropriately

## Future Considerations

1. Extended AI capabilities
2. Additional data format support
3. Enhanced security features
4. Improved validation tools
5. Extended command set

Enter `/help` to see what AI can do.
