# OGSP Recipe Representation Specification (v2.1)

*This document is part of the OGSP 2.0 specification suite. For the overarching vision, motivation, and community-driven approach, please refer to the [Root Specification](../ogsp-root-spec.md).*

## Introduction
This document specifies the format and structure for representing growing recipes within the OGSP protocol. It aims to provide a standardized approach for defining, sharing, and executing recipes across diverse hardware and software environments.

The OGSP Recipe Specification has been enhanced to support a comprehensive entity model and automation framework, enabling sophisticated interactions between sensors, actuators, and virtual entities, as well as complex automation workflows triggered by events.

## Versioning
- Current Version: 2.1.0

## References
- [Root Specification](../ogsp-root-spec.md)
- [Core Protocol Specification](../core/ogsp-core-spec.md)
- [Hardware Abstraction Specification](../hardware/ogsp-hardware-spec.md)
- [AI Integration Specification](../ai/ogsp-ai-spec.md)
- [Security Specification](../security/ogsp-security-spec.md)

## Core Concepts

### Metadata
- **Identification**: Unique ID, Name, and Description
- **Versioning**: Semantic versioning (MAJOR.MINOR.PATCH)
- **Ownership**: Author and Licensing Information
- **Provenance**: Origin and Modification History
- **Lineage**: Parent recipe ID and fork history
- **Signatures**: Digital signatures for verification
- **Access Control**: Permissions and sharing settings

### Phases
- **Sequence**: Ordered steps for growth
- **Conditions**: Environmental and temporal conditions
- **Error Handling**: Procedures for handling deviations

### Resources
- **Inputs**: Required materials and quantities
- **Outputs**: Expected results and by-products
- **Dependencies**: Inter-recipe and external dependencies

### Environment
- **Requirements**: Hardware and software prerequisites
- **Constraints**: Limitations and safety considerations
- **Capability Matching**: Hardware capability profiles
- **Fallback Mechanisms**: Alternative implementations
- **Performance Profiles**: Expected performance metrics

### Entity Model
- **Entity Types**: Sensors, actuators, and virtual entities
- **Entity Capabilities**: Specifications and operational parameters
- **Entity Relationships**: Connections and interactions between entities
- **Virtual Entities**: AI-based processors and derived data sources

### Automation Framework
- **Events**: Triggers based on conditions, time, or state changes
- **Actions**: Operations to perform in response to events
- **Rules**: Mappings between events and actions with conditions
- **Workflows**: Complex sequences of actions with dependencies

### Validation
- **Schema Conformance**: Adherence to defined schema
- **Business Rules**: Logical consistency and constraints
- **Error Reporting**: Detailed error messages and locations
- **Integrity Checks**: Digital signature verification
- **Access Control**: Permission validation
- **AI Validation**: Confidence scoring and explainability

## Entity Model

The Entity Model provides a structured way to represent physical and virtual components within a growing system. This model enables recipes to define the entities involved in the growing process, their capabilities, and their relationships.

### Entity Types

#### Sensors
Sensors are physical devices that collect data from the environment. They are defined with the following attributes:

```json
{
  "id": "temperature-sensor-1",
  "type": "environmental-temperature",
  "capabilities": {
    "accuracy": 0.5,
    "range": {"min": -10, "max": 50},
    "resolution": 0.1,
    "units": "celsius"
  },
  "placement": "grow-room-main",
  "sampleRate": "60s"
}
```

Sensor types include:
- **Environmental Sensors**: Temperature, humidity, light, CO2, etc.
- **Substrate Sensors**: Moisture, pH, EC, etc.
- **Plant Sensors**: Weight, size, color, etc.
- **Resource Sensors**: Water level, nutrient levels, etc.

#### Actuators
Actuators are physical devices that modify the environment. They are defined with the following attributes:

```json
{
  "id": "hvac-1",
  "type": "environmental-temperature-control",
  "capabilities": {
    "range": {"min": 15, "max": 35},
    "resolution": 0.5,
    "rampRate": "2C/min"
  },
  "placement": "grow-room-main",
  "controlMode": "pid"
}
```

Actuator types include:
- **Environmental Control**: HVAC, lighting, CO2 injection, etc.
- **Irrigation and Nutrient Delivery**: Pumps, valves, mixers, etc.
- **Mechanical Systems**: Pruning, harvesting, etc.
- **Notification Systems**: Alarms, indicators, etc.

#### Virtual Entities
Virtual entities are software-based components that process data or provide derived functionality. They are defined with the following attributes:

```json
{
  "id": "plant-health-monitor",
  "type": "ai-processor",
  "inputs": ["camera-1"],
  "capabilities": {
    "detects": ["leaf-discoloration", "pest-presence", "growth-rate"],
    "confidenceThreshold": 0.85,
    "updateInterval": "6h"
  },
  "model": {
    "name": "cannabis-health-v2",
    "version": "2.1.0",
    "trainingData": "50k cannabis plants across 20 strains"
  }
}
```

Virtual entity types include:
- **AI Processors**: Machine learning models that analyze data
- **Aggregated Sensors**: Virtual sensors that combine data from multiple sources
- **Controller Entities**: Logical controllers for complex processes
- **Metric Generators**: Components that calculate derived metrics

### Entity Relationships

Entity relationships define how entities interact with each other. They are defined with the following attributes:

```json
{
  "sourceEntity": "temperature-sensor-1",
  "targetEntity": "hvac-1",
  "relationshipType": "monitors-for",
  "parameters": {
    "feedbackLoop": true,
    "priority": "high"
  }
}
```

Relationship types include:
- **monitors-for**: A sensor monitors conditions for an actuator
- **controls**: An actuator controls an aspect of the environment
- **data-source-for**: An entity provides data to another entity
- **depends-on**: An entity depends on another entity for operation
- **aggregates**: An entity aggregates data from multiple sources

## Automation Framework

The Automation Framework provides a structured way to define how a growing system should respond to events and conditions. This framework enables recipes to specify complex automation workflows that can adapt to changing conditions.

### Events

Events are triggers that initiate automation processes. They are categorized into several types:

#### Threshold Events
Triggered when a sensor value crosses a threshold:

```json
{
  "id": "high-temp-alert",
  "source": "temperature-sensor-1",
  "condition": {
    "parameter": "temperature",
    "operator": ">",
    "value": 30,
    "duration": "5m"
  },
  "severity": "warning"
}
```

#### Time Events
Triggered at specific times or on schedules:

```json
{
  "id": "light-schedule-on",
  "schedule": "0 6 * * *",
  "phase": ["vegetative", "flowering"],
  "description": "Daily lights on at 6am"
}
```

#### State Events
Triggered when an entity changes state:

```json
{
  "id": "phase-transition",
  "source": "recipe-engine",
  "fromState": "vegetative",
  "toState": "flowering",
  "description": "Plants entering flowering phase"
}
```

#### Compound Events
Triggered by combinations of other events:

```json
{
  "id": "stress-condition",
  "operator": "AND",
  "events": ["high-temp-alert", "low-humidity-alert"],
  "window": "10m",
  "description": "Environmental stress combination"
}
```

### Actions

Actions are operations that are performed in response to events. They are categorized into several types:

#### Control Actions
Actions that control actuators:

```json
{
  "id": "reduce-temperature",
  "target": "hvac-1",
  "command": "set-temperature",
  "parameters": {
    "temperature": "{{current_temperature - 3}}",
    "mode": "cooling"
  },
  "constraints": {
    "minValue": 18,
    "maxAdjustment": 5
  }
}
```

#### Notification Actions
Actions that send notifications:

```json
{
  "id": "alert-grower",
  "channels": ["app-notification", "email"],
  "message": "High temperature condition detected: {{temperature}}°C",
  "urgency": "{{severity}}"
}
```

#### Adjustment Actions
Actions that make adjustments to system parameters:

```json
{
  "id": "transition-light-schedule",
  "target": "lighting-controller",
  "parameters": {
    "hoursOn": 12,
    "spectrum": "flowering",
    "intensity": "80%",
    "transitionDays": 7
  }
}
```

### Automation Rules

Automation rules map events to actions with conditions:

```json
{
  "id": "temp-control-rule",
  "description": "Maintain temperature in optimal range",
  "trigger": "high-temp-alert",
  "conditions": [
    {
      "entity": "outside-temp-sensor",
      "parameter": "temperature",
      "operator": ">",
      "value": 25
    }
  ],
  "actions": [
    {
      "action": "reduce-temperature",
      "order": 1
    },
    {
      "action": "alert-grower",
      "order": 2,
      "conditions": [
        {
          "parameter": "severity",
          "operator": "==",
          "value": "critical"
        }
      ]
    }
  ],
  "cooldown": "10m"
}
```

### Workflows

Workflows define complex sequences of actions with dependencies:

```json
{
  "id": "phase-transition-workflow",
  "description": "Transition from vegetative to flowering phase",
  "trigger": "phase-transition",
  "steps": [
    {
      "id": "step-1",
      "action": "transition-light-schedule",
      "waitFor": "complete"
    },
    {
      "id": "step-2",
      "action": "adjust-nutrient-mix",
      "parameters": {
        "formula": "flowering-stage"
      },
      "waitFor": "3d"
    },
    {
      "id": "step-3",
      "action": "reduce-temperature",
      "parameters": {
        "temperature": 24
      },
      "waitFor": "complete"
    }
  ],
  "errorHandling": {
    "onFailure": "alert-grower",
    "retryStrategy": {
      "maxAttempts": 3,
      "backoff": "exponential"
    }
  }
}
```

## Recipe Versioning and Forking

Recipes MUST include semantic versioning (MAJOR.MINOR.PATCH) following these rules:
1. MAJOR version changes when incompatible changes are made
2. MINOR version changes when functionality is added in a backward-compatible manner
3. PATCH version changes when backward-compatible bug fixes are implemented

Forked recipes MUST:
1. Include parent recipe ID
2. Maintain complete modification history
3. Preserve original signatures
4. Track lineage through fork chain

Systems MUST check version compatibility before execution and MUST validate recipe lineage.

## Recipe Validation

Growing systems MUST validate recipes before execution, checking:
1. Schema conformance
2. Internal consistency
3. Hardware compatibility
4. Safety parameters
5. Resource requirements
6. Digital signatures
7. Access permissions
8. AI confidence scores
9. Explainability documentation
10. Entity relationships validity
11. Automation rule consistency
12. Workflow integrity

Validation failures MUST be reported with clear error messages indicating:
1. The specific issue
2. Its location within the recipe
3. Suggested remediation steps
4. Impact assessment

## GitHub Repository Structure

To support the open source philosophy and enable effective sharing and collaboration, OGSP recipes should be organized in GitHub repositories following a standardized structure:

```
recipe-repository/
├── README.md                 # Overview, usage instructions, and documentation
├── recipe.json               # The main recipe file
├── LICENSE                   # License information
├── CHANGELOG.md              # Version history and changes
├── entities/                 # Entity definitions
│   ├── sensors.json          # Sensor entity definitions
│   ├── actuators.json        # Actuator entity definitions
│   └── virtual-entities.json # Virtual entity definitions
├── automations/              # Automation definitions
│   ├── events.json           # Event definitions
│   ├── actions.json          # Action definitions
│   ├── rules.json            # Rule definitions
│   └── workflows.json        # Workflow definitions
├── media/                    # Images, videos, and other media
│   ├── images/               # Plant images, diagrams, etc.
│   └── videos/               # Growing process videos, etc.
├── data/                     # Example data and results
│   ├── sample-runs/          # Data from sample runs
│   └── expected-results/     # Expected outcomes
└── docs/                     # Additional documentation
    ├── setup.md              # Setup instructions
    ├── troubleshooting.md    # Troubleshooting guide
    └── advanced-usage.md     # Advanced usage information
```

This structure enables:
1. Clear organization of recipe components
2. Easy discovery of recipe capabilities
3. Effective collaboration through pull requests
4. Version tracking through Git
5. Documentation alongside code
6. Reuse of components across recipes

## Implementation Examples

### Cannabis Growing Example

The following example demonstrates a recipe for growing cannabis with automated environmental control:

```json
{
  "version": "2.1.0",
  "metadata": {
    "id": "550e8400-e29b-41d4-a716-446655440000",
    "name": "Emerald Dream Cannabis Strain",
    "author": "GreenThumb420",
    "created": "2025-03-19T02:40:00Z",
    "parentId": "550e8400-e29b-41d4-a716-446655440001",
    "signatures": [
      {
        "signer": "GreenThumb420",
        "timestamp": "2025-03-19T02:40:00Z",
        "signature": "a1b2c3d4e5f6g7h8i9j0"
      }
    ],
    "accessControl": {
      "permissions": [
        {
          "entity": "user:GreenThumb420",
          "actions": ["read", "write", "execute", "fork"]
        },
        {
          "entity": "group:OGSP-Community",
          "actions": ["read", "fork"]
        }
      ]
    }
  },
  "phases": [
    {
      "name": "Germination",
      "duration": {
        "value": 3,
        "unit": "days"
      },
      "conditions": {
        "temperature": {
          "min": 22,
          "max": 25
        },
        "humidity": {
          "min": 70,
          "max": 80
        }
      }
    },
    {
      "name": "Vegetative",
      "duration": {
        "value": 4,
        "unit": "weeks"
      },
      "conditions": {
        "temperature": {
          "min": 20,
          "max": 28
        },
        "humidity": {
          "min": 40,
          "max": 70
        }
      }
    },
    {
      "name": "Flowering",
      "duration": {
        "value": 8,
        "unit": "weeks"
      },
      "conditions": {
        "temperature": {
          "min": 18,
          "max": 26
        },
        "humidity": {
          "min": 40,
          "max": 50
        }
      }
    }
  ],
  "entities": {
    "sensors": [
      {
        "id": "temp-sensor-1",
        "type": "environmental-temperature",
        "capabilities": {
          "accuracy": 0.5,
          "range": {"min": -10, "max": 50},
          "resolution": 0.1,
          "units": "celsius"
        },
        "placement": "grow-room-main",
        "sampleRate": "60s"
      },
      {
        "id": "humidity-sensor-1",
        "type": "environmental-humidity",
        "capabilities": {
          "accuracy": 2.0,
          "range": {"min": 0, "max": 100},
          "resolution": 0.5,
          "units": "percent"
        },
        "placement": "grow-room-main",
        "sampleRate": "60s"
      },
      {
        "id": "camera-1",
        "type": "plant-camera",
        "capabilities": {
          "resolution": "4K",
          "spectrum": ["visible", "infrared"],
          "frameRate": "1/hour"
        },
        "placement": "grow-room-ceiling",
        "sampleRate": "1h"
      }
    ],
    "actuators": [
      {
        "id": "hvac-1",
        "type": "environmental-temperature-control",
        "capabilities": {
          "range": {"min": 15, "max": 35},
          "resolution": 0.5,
          "rampRate": "2C/min"
        },
        "placement": "grow-room-main",
        "controlMode": "pid"
      },
      {
        "id": "humidifier-1",
        "type": "environmental-humidity-control",
        "capabilities": {
          "range": {"min": 30, "max": 90},
          "resolution": 1.0,
          "capacity": "5L/day"
        },
        "placement": "grow-room-main",
        "controlMode": "on-off"
      },
      {
        "id": "lighting-1",
        "type": "lighting-control",
        "capabilities": {
          "spectrum": ["full-spectrum", "vegetative", "flowering"],
          "intensity": {"min": 0, "max": 100, "unit": "percent"},
          "coverage": "2m x 2m"
        },
        "placement": "grow-room-ceiling",
        "controlMode": "scheduled"
      }
    ],
    "virtualEntities": [
      {
        "id": "plant-health-monitor",
        "type": "ai-processor",
        "inputs": ["camera-1"],
        "capabilities": {
          "detects": ["leaf-discoloration", "pest-presence", "growth-rate"],
          "confidenceThreshold": 0.85,
          "updateInterval": "6h"
        },
        "model": {
          "name": "cannabis-health-v2",
          "version": "2.1.0",
          "trainingData": "50k cannabis plants across 20 strains"
        }
      },
      {
        "id": "vpd-calculator",
        "type": "metric-generator",
        "inputs": ["temp-sensor-1", "humidity-sensor-1"],
        "capabilities": {
          "metrics": ["vapor-pressure-deficit"],
          "updateInterval": "5m"
        }
      }
    ]
  },
  "entityRelationships": [
    {
      "sourceEntity": "temp-sensor-1",
      "targetEntity": "hvac-1",
      "relationshipType": "monitors-for",
      "parameters": {
        "feedbackLoop": true,
        "priority": "high"
      }
    },
    {
      "sourceEntity": "humidity-sensor-1",
      "targetEntity": "humidifier-1",
      "relationshipType": "monitors-for",
      "parameters": {
        "feedbackLoop": true,
        "priority": "medium"
      }
    },
    {
      "sourceEntity": "camera-1",
      "targetEntity": "plant-health-monitor",
      "relationshipType": "data-source-for",
      "parameters": {
        "dataFormat": "image/jpeg",
        "resolution": "4K"
      }
    },
    {
      "sourceEntity": "temp-sensor-1",
      "targetEntity": "vpd-calculator",
      "relationshipType": "data-source-for",
      "parameters": {
        "metric": "temperature"
      }
    },
    {
      "sourceEntity": "humidity-sensor-1",
      "targetEntity": "vpd-calculator",
      "relationshipType": "data-source-for",
      "parameters": {
        "metric": "humidity"
      }
    }
  ],
  "events": {
    "thresholdEvents": [
      {
        "id": "high-temp-alert",
        "source": "temp-sensor-1",
        "condition": {
          "parameter": "temperature",
          "operator": ">",
          "value": 30,
          "duration": "5m"
        },
        "severity": "warning"
      },
      {
        "id": "low-humidity-alert",
        "source": "humidity-sensor-1",
        "condition": {
          "parameter": "humidity",
          "operator": "<",
          "value": 35,
          "duration": "10m"
        },
        "severity": "warning"
      },
      {
        "id": "vpd-out-of-range",
        "source": "vpd-calculator",
        "condition": {
          "parameter": "vapor-pressure-deficit",
          "operator": "outside",
          "value": {"min": 0.8, "max": 1.2},
          "duration": "30m"
        },
        "severity": "info"
      }
    ],
    "timeEvents": [
      {
        "id": "lights-on",
        "schedule": "0 6 * * *",
        "phase": ["vegetative", "flowering"],
        "description": "Daily lights on at 6am"
      },
      {
        "id": "lights-off-veg",
        "schedule": "0 0 * * *",
        "phase": ["vegetative"],
        "description": "Lights off at midnight during vegetative phase"
      },
      {
        "id": "lights-off-flower",
        "schedule": "0 18 * * *",
        "phase": ["flowering"],
        "description": "Lights off at 6pm during flowering phase"
      }
    ],
    "stateEvents": [
      {
        "id": "veg-to-flower",
        "source": "recipe-engine",
        "fromState": "vegetative",
        "toState": "flowering",
        "description": "Transition from vegetative to flowering phase"
      }
    ],
    "compoundEvents": [
      {
        "id": "environmental-stress",
        "operator": "AND",
        "events": ["high-temp-alert", "low-humidity-alert"],
        "window": "15m",
        "description": "Combined temperature and humidity stress"
      }
    ]
  },
  "actions": {
    "controlActions": [
      {
        "id": "cool-room",
        "target": "hvac-1",
        "command": "set-temperature",
        "parameters": {
          "temperature": "{{current_temperature - 2}}",
          "mode": "cooling"
        },
        "constraints": {
          "minValue": 18,
          "maxAdjustment": 5
        }
      },
      {
        "id": "increase-humidity",
        "target": "humidifier-1",
        "command": "set-humidity",
        "parameters": {
          "humidity": "{{current_humidity + 10}}",
          "mode": "continuous"
        },
        "constraints": {
          "maxValue": 70
        }
      },
      {
        "id": "set-light-schedule-veg",
        "target": "lighting-1",
        "command": "set-schedule",
        "parameters": {
          "onTime": "06:00",
          "offTime": "00:00",
          "spectrum": "vegetative",
          "intensity": 80
        }
      },
      {
        "id": "set-light-schedule-flower",
        "target": "lighting-1",
        "command": "set-schedule",
        "parameters": {
          "onTime": "06:00",
          "offTime": "18:00",
          "spectrum": "flowering",
          "intensity": 90
        }
      }
    ],
    "notificationActions": [
      {
        "id": "alert-environmental-issue",
        "channels": ["app-notification", "email"],
        "message": "Environmental issue detected: {{event_description}}. Current values: Temperature {{temperature}}°C, Humidity {{humidity}}%",
        "urgency": "{{severity}}"
      },
      {
        "id": "notify-phase-change",
        "channels": ["app-notification"],
        "message": "Plants have entered {{toState}} phase. Adjusting environmental parameters.",
        "urgency": "info"
      }
    ],
    "adjustmentActions": [
      {
        "id": "optimize-vpd",
        "target": "environment-controller",
        "parameters": {
          "targetVPD": 1.0,
          "adjustmentPriority": "temperature",
          "adjustmentRate": "gradual"
        }
      }
    ]
  },
  "automationRules": [
    {
      "id": "high-temp-response",
      "description": "Respond to high temperature conditions",
      "trigger": "high-temp-alert",
      "conditions": [],
      "actions": [
        {
          "action": "cool-room",
          "order": 1
        },
        {
          "action": "alert-environmental-issue",
          "order": 2
        }
      ],
      "cooldown": "15m"
    },
    {
      "id": "low-humidity-response",
      "description": "Respond to low humidity conditions",
      "trigger": "low-humidity-alert",
      "conditions": [],
      "actions": [
        {
          "action": "increase-humidity",
          "order": 1
        },
        {
          "action": "alert-environmental-issue",
          "order": 2
        }
      ],
      "cooldown": "15m"
    },
    {
      "id": "vpd-optimization",
      "description": "Optimize vapor pressure deficit",
      "trigger": "vpd-out-of-range",
      "conditions": [],
      "actions": [
        {
          "action": "optimize-vpd",
          "order": 1
        }
      ],
      "cooldown": "1h"
    }
  ],
  "workflows": [
    {
      "id": "veg-to-flower-transition",
      "description": "Transition from vegetative to flowering phase",
      "trigger": "veg-to-flower",
      "steps": [
        {
          "id": "step-1",
          "action": "set-light-schedule-flower",
          "waitFor": "complete"
        },
        {
          "id": "step-2",
          "action": "optimize-vpd",
          "parameters": {
            "targetVPD": 0.9
          },
          "waitFor": "2d"
        },
        {
          "id": "step-3",
          "action": "notify-phase-change",
          "waitFor": "complete"
        }
      ],
      "errorHandling": {
        "onFailure": "alert-environmental-issue",
        "retryStrategy": {
          "maxAttempts": 3,
          "backoff": "exponential"
        }
      }
    }
  ],
  "hardware": {
    "capabilities": [
      {
        "type": "temperature-control",
        "min": 15,
        "max": 35
      },
      {
        "type": "humidity-control",
        "min": 30,
        "max": 90
      },
      {
        "type": "lighting-control",
        "spectrum": ["full-spectrum", "vegetative", "flowering"]
      }
    ],
    "fallbacks": [
      {
        "condition": "temperature > 32",
        "action": "emergency-cooling"
      },
      {
        "condition": "humidity > 85",
        "action": "emergency-dehumidify"
      }
    ],
    "performance": {
      "expected": {
        "yield": 500,
        "duration": 90
      },
      "tolerance": 0.1
    }
  },
  "ai": {
    "confidence": 0.92,
    "explanation": "This recipe has been validated against 120 similar strains with 92% success rate. Key factors: stable temperature control, precise humidity management, and optimized light cycles for this specific strain."
  }
}
```

This example demonstrates how the enhanced recipe protocol can represent a comprehensive growing system with sensors, actuators, virtual entities, and automation workflows.
