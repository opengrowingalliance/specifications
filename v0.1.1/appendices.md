# Appendices

## Appendix B: Complete Recipe Schema Reference

### Overview
The OGSP Recipe Schema defines the structure and validation rules for growth recipes used within the Open Growing System Protocol. This schema ensures that recipes are consistent, valid, and can be processed by compliant systems.

### Schema Definition
The schema is defined in JSON Schema format and includes the following key components:

- **Version**: A string indicating the schema version, following the pattern `MAJOR.MINOR.PATCH`.
- **Metadata**: An object containing essential information about the recipe, including:
  - **Name**: The name of the recipe (required).
  - **Author**: The author of the recipe.
  - **Created**: The date and time when the recipe was created, formatted as a date-time string.

- **Phases**: An array of phase objects, each representing a distinct stage in the plant's growth cycle. Each phase includes:
  - **Name**: The name of the phase (required).
  - **Duration**: An object specifying the duration of the phase, which includes:
    - **Value**: A numeric value representing the duration.
    - **Unit**: A string indicating the unit of time (must be one of "days", "weeks", or "months").

### Phase Definition
Each phase object must include the following properties:
- **Conditions**: An object defining the environmental conditions required for the phase, including:
  - **Temperature**: An object with minimum and maximum temperature values.
  - **Humidity**: An object with minimum and maximum humidity values.

### Example Recipe Schema
```json
{
  "version": "1.0.0",
  "metadata": {
    "name": "Basic Tomato Grow",
    "author": "Open Growing Alliance",
    "created": "2025-03-18T00:00:00Z"
  },
  "phases": [
    {
      "name": "seedling",
      "duration": {
        "value": 14,
        "unit": "days"
      },
      "conditions": {
        "temperature": {
          "min": 18,
          "max": 28
        },
        "humidity": {
          "min": 40,
          "max": 70
        }
      }
    }
  ]
}
```

### Validation Rules
- All recipes must conform to the schema defined above.
- Validation errors must be reported with clear messages indicating the specific issue and its location within the recipe.

## Appendix C: Entity Relationship Diagram
*To be developed.*

## Appendix D: Command Reference
*To be developed.*

## Appendix E: Event Reference
*To be developed.*

## Appendix F: Error Codes and Handling

### Error Codes
The following error codes are used within the OGSP to indicate specific issues:

- **1000**: Invalid Schema - The provided data does not conform to the required schema.
- **1001**: Missing Required Field - A required field is missing from the data.
- **1002**: Invalid Data Type - The data type of a field is incorrect.
- **1003**: Out of Range - A numeric value is outside the allowed range.
- **1004**: Unsupported Operation - The requested operation is not supported.

### Error Handling
Errors should be handled gracefully by the system, providing clear and actionable feedback to the user. The following guidelines should be followed:

1. **Logging**: All errors should be logged with sufficient detail to diagnose the issue.
2. **User Feedback**: Users should receive a clear error message indicating the nature of the problem and potential steps to resolve it.
3. **Retry Mechanism**: For transient errors, the system should implement a retry mechanism with exponential backoff.
4. **Alerting**: Critical errors should trigger alerts to the system administrators for immediate attention.


## Appendix G: Example AI Model Integration
*To be developed.*
