# OGSP Recipe Representation Specification (v2.2)

*This document is part of the OGSP 2.0 specification suite. For the overarching vision, motivation, and community-driven approach, please refer to the [Root Specification](../ogsp-root-spec.md).*

## Introduction
This document specifies the format and structure for representing growing recipes within the OGSP protocol. It aims to provide a standardized approach for defining, sharing, and executing recipes across diverse hardware and software environments.

The OGSP Recipe Specification has been enhanced to emphasize a declarative approach to recipe definition, focusing on plant needs rather than implementation details. This revision strengthens the separation between "what" a plant needs and "how" a system implements those needs, making recipes more portable and adaptable across different growing systems.

## Versioning
- Current Version: 2.2.0
- Previous Version: 2.1.0

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
- **Declarative Definition**: Plant-centric description of growth phases
- **Environmental Requirements**: Optimal and acceptable ranges for all parameters
- **Biological Context**: Explanation of plant needs and development during each phase
- **Success Criteria**: Clear markers for successful phase completion
- **Common Issues**: Potential problems and their prevention

### Resources
- **Inputs**: Required materials and quantities
- **Outputs**: Expected results and by-products
- **Dependencies**: Inter-recipe and external dependencies

### Implementation Guidance
- **Hardware Requirements**: Suggested capabilities for implementation
- **Adaptation Guidelines**: How to adapt the recipe to different systems
- **Fallback Mechanisms**: Alternative approaches when optimal conditions can't be met
- **Performance Expectations**: Expected outcomes under various conditions

### Validation
- **Schema Conformance**: Adherence to defined schema
- **Business Rules**: Logical consistency and constraints
- **Error Reporting**: Detailed error messages and locations
- **Integrity Checks**: Digital signature verification
- **Access Control**: Permission validation
- **AI Validation**: Confidence scoring and explainability

## Declarative Phase Model

The Declarative Phase Model provides a structured way to represent plant growth phases based on plant needs rather than system implementation. This model enables recipes to define what plants need during each growth phase without prescribing how those needs should be met.

### Phase Structure

A growth phase is defined with the following attributes:

```yaml
name: "Vegetative"
description: "Growth phase focused on leaf and stem development"
typicalDuration:
  value: 4
  unit: "weeks"
  variabilityFactors: ["strain genetics", "desired plant size", "growing conditions"]
environment:
  temperature:
    day:
      optimal: 24
      range:
        min: 20
        max: 28
    night:
      optimal: 20
      range:
        min: 18
        max: 24
    stability:
      maxVariation: 5
      period: "day"
  humidity:
    optimal: 60
    range:
      min: 40
      max: 70
    stability:
      maxVariation: 10
      period: "day"
    trend:
      direction: "decreasing"
      rate: "gradual"
  light:
    dailyDuration:
      hours: 18
    intensity:
      optimal: "medium"
      range:
        min: 300
        max: 600
        unit: "PPFD"
    spectrum:
      primary: "blue"
      secondary: "red"
      ratios:
        blue:red: 1.5
  substrate:
    moisture:
      optimal: 60
      range:
        min: 40
        max: 70
      cycle: "wet-to-moderate dry"
    temperature:
      optimal: 22
      range:
        min: 18
        max: 26
  air:
    co2:
      optimal: 800
      range:
        min: 600
        max: 1200
        unit: "ppm"
    movement:
      optimal: "moderate"
      description: "Continuous gentle breeze to strengthen stems"
nutrition:
  profile: "nitrogen-dominant"
  macroNutrients:
    N:
      optimal: "high"
      range:
        min: 150
        max: 250
        unit: "ppm"
    P:
      optimal: "medium"
      range:
        min: 50
        max: 80
        unit: "ppm"
    K:
      optimal: "medium"
      range:
        min: 100
        max: 150
        unit: "ppm"
  microNutrients: "standard cannabis profile"
  ec:
    optimal: 1.2
    range:
      min: 0.8
      max: 1.6
      unit: "mS/cm"
  ph:
    optimal: 6.0
    range:
      min: 5.8
      max: 6.3
successCriteria:
  primary: "Robust vegetative growth with strong branches and healthy foliage"
  secondaryMarkers: ["internodal spacing", "leaf size", "stem thickness"]
  healthIndicators: ["deep green leaves", "upward growth", "vigorous new shoots"]
stressSensitivity:
  temperature: "moderate"
  underwatering: "moderate"
  overwatering: "moderate"
  nutrientDeficiency: "high"
commonIssues:
  - name: "Nitrogen deficiency"
    symptoms: ["yellowing of older leaves", "stunted growth"]
    causes: ["insufficient nitrogen", "pH imbalance", "root problems"]
    preventions: ["proper nutrient solution", "regular pH monitoring", "healthy root zone"]
```

### Phase Types

Common phase types include:

- **Germination/Propagation**: Initial growth from seed or cutting
- **Establishment**: Early growth and root development
- **Vegetative**: Focus on leaf and stem growth
- **Transition**: Preparation for flowering or fruiting
- **Flowering/Fruiting**: Reproductive phase
- **Ripening/Maturation**: Final development before harvest
- **Senescence**: End-of-life phase (for perennial plants)

### Environmental Parameters

Environmental parameters are defined in terms of plant needs rather than system settings:

#### Temperature
```yaml
temperature:
  day:
    optimal: 24
    range:
      min: 20
      max: 28
  night:
    optimal: 20
    range:
      min: 18
      max: 24
  stability:
    maxVariation: 5
    period: "day"
  biologicalContext: "Higher daytime temperatures support photosynthesis while cooler nights reduce respiration and conserve energy"
```

#### Humidity
```yaml
humidity:
  optimal: 60
  range:
    min: 40
    max: 70
  stability:
    maxVariation: 10
    period: "day"
  trend:
    direction: "decreasing"
    rate: "gradual"
  biologicalContext: "Higher humidity supports vegetative growth while gradual reduction prepares plants for flowering"
```

#### Light
```yaml
light:
  dailyDuration:
    hours: 18
  intensity:
    optimal: "medium"
    range:
      min: 300
      max: 600
      unit: "PPFD"
  spectrum:
    primary: "blue"
    secondary: "red"
    ratios:
      blue:red: 1.5
  biologicalContext: "Blue-dominant spectrum promotes vegetative growth and compact structure"
```

#### Substrate
```yaml
substrate:
  moisture:
    optimal: 60
    range:
      min: 40
      max: 70
    cycle: "wet-to-moderate dry"
  temperature:
    optimal: 22
    range:
      min: 18
      max: 26
  biologicalContext: "Allowing substrate to partially dry between waterings promotes oxygen in the root zone and stronger root development"
```

#### Air
```yaml
air:
  co2:
    optimal: 800
    range:
      min: 600
      max: 1200
      unit: "ppm"
  movement:
    optimal: "moderate"
    description: "Continuous gentle breeze to strengthen stems"
  biologicalContext: "Elevated CO2 increases photosynthetic efficiency while air movement strengthens stems and reduces pest pressure"
```

### Nutrition

Nutrition is defined in terms of plant requirements rather than specific nutrient solutions:

```yaml
nutrition:
  profile: "nitrogen-dominant"
  macroNutrients:
    N:
      optimal: "high"
      range:
        min: 150
        max: 250
        unit: "ppm"
    P:
      optimal: "medium"
      range:
        min: 50
        max: 80
        unit: "ppm"
    K:
      optimal: "medium"
      range:
        min: 100
        max: 150
        unit: "ppm"
  microNutrients: "standard cannabis profile"
  ec:
    optimal: 1.2
    range:
      min: 0.8
      max: 1.6
      unit: "mS/cm"
  ph:
    optimal: 6.0
    range:
      min: 5.8
      max: 6.3
  biologicalContext: "Nitrogen-dominant nutrition supports vegetative growth and leaf development"
```

### Success Criteria

Success criteria define what successful completion of a phase looks like from a plant perspective:

```yaml
successCriteria:
  primary: "Robust vegetative growth with strong branches and healthy foliage"
  secondaryMarkers: ["internodal spacing", "leaf size", "stem thickness"]
  healthIndicators: ["deep green leaves", "upward growth", "vigorous new shoots"]
  readinessForNextPhase: "When plant has reached desired size and structure, typically 30-45cm tall with 6-8 node sites"
```

### Stress Sensitivity

Stress sensitivity indicates which environmental factors the plant is most sensitive to during each phase:

```yaml
stressSensitivity:
  temperature: "moderate"
  underwatering: "moderate"
  overwatering: "moderate"
  nutrientDeficiency: "high"
  light: "low"
  prioritization: "During this phase, maintaining proper nutrition is most critical, followed by water management"
```

### Common Issues

Common issues provide information about problems that might occur during a phase:

```yaml
commonIssues:
  - name: "Nitrogen deficiency"
    symptoms: ["yellowing of older leaves", "stunted growth"]
    causes: ["insufficient nitrogen", "pH imbalance", "root problems"]
    preventions: ["proper nutrient solution", "regular pH monitoring", "healthy root zone"]
    corrections: ["increase nitrogen in nutrient solution", "check and adjust pH", "examine roots for health issues"]
```

## Phase Transitions

Phase transitions define how plants move from one growth phase to another:

```yaml
transitions:
  - from: "Vegetative"
    to: "Flowering"
    trigger:
      type: "time-based"
      condition: "after 4 weeks of vegetative growth"
      alternativeTriggers: ["plant height reaches 40cm", "8 node sites developed"]
    environmentalShift:
      light:
        dailyDuration:
          from: 18
          to: 12
          unit: "hours"
        spectrum:
          from: "blue-dominant"
          to: "red-dominant"
        transitionPeriod:
          value: 7
          unit: "days"
      nutrition:
        profile:
          from: "nitrogen-dominant"
          to: "phosphorus-dominant"
        transitionPeriod:
          value: 7
          unit: "days"
    biologicalContext: "Reducing light hours triggers hormonal changes that shift the plant from vegetative growth to flowering"
```

## Implementation Guidance

The Implementation Guidance section provides suggestions for how growing systems might implement the recipe, without prescribing specific hardware or methods:

```yaml
implementationGuidance:
  hardwareCapabilities:
    temperature:
      controlRange:
        min: 15
        max: 35
      precision: 1.0
    humidity:
      controlRange:
        min: 30
        max: 90
      precision: 5.0
    lighting:
      spectrumControl: "recommended"
      intensityControl: "required"
  adaptationGuidelines:
    limitedCapabilities:
      noSpectrumControl: "Focus on light duration control and use full-spectrum lights"
      limitedHumidityControl: "Prioritize ventilation during high humidity periods and misting during low humidity"
    resourceConstraints:
      energyEfficiency: "Reduce light intensity by 10% with 15% longer growth period"
      waterConservation: "Reduce irrigation frequency with deeper watering"
  fallbackMechanisms:
    environmentalControl:
      temperatureExcursion: "Prioritize air movement and adjust light intensity"
      humidityExcursion: "Modify ventilation and irrigation timing"
```

## Separation of Concerns

The revised specification maintains a clear separation between:

1. **Declarative Plant Needs**: What the plant requires during each growth phase
2. **Implementation Guidance**: Suggestions for how systems might meet those needs
3. **System-Specific Implementation**: How a particular system implements the recipe

This separation ensures that recipes remain portable across different growing systems while providing sufficient guidance for successful implementation.

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
10. Phase definition completeness
11. Transition logic consistency
12. Success criteria clarity

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
├── recipe.yaml               # The main recipe file
├── LICENSE                   # License information
├── CHANGELOG.md              # Version history and changes
├── phases/                   # Detailed phase definitions
│   ├── germination.yaml      # Germination phase details
│   ├── vegetative.yaml       # Vegetative phase details
│   └── flowering.yaml        # Flowering phase details
├── transitions/              # Phase transition definitions
│   ├── germ-to-veg.yaml      # Germination to vegetative transition
│   └── veg-to-flower.yaml    # Vegetative to flowering transition
├── implementation/           # Implementation guidance
│   ├── hardware-profiles/    # Hardware capability profiles
│   ├── adaptation-guides/    # Adaptation guidelines
│   └── fallbacks/            # Fallback mechanisms
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

## Implementation Example

Below is a simplified example of a declarative recipe for cannabis cultivation:

```yaml
version: "2.2.0"
metadata:
  id: "550e8400-e29b-41d4-a716-446655440000"
  name: "Emerald Dream Cannabis Strain"
  author: "GreenThumb420"
  created: "2025-03-19T04:00:00Z"
phases:
  - name: "Germination"
    description: "Initial sprouting phase"
    typicalDuration:
      value: 3
      unit: "days"
    environment:
      temperature:
        optimal: 24
        range:
          min: 22
          max: 25
        biologicalContext: "Activates enzymes needed for germination"
      humidity:
        optimal: 75
        range:
          min: 70
          max: 80
        biologicalContext: "Prevents seed desiccation"
    successCriteria:
      primary: "Emergence of radicle and cotyledons"
      readinessForNextPhase: "When cotyledons are fully expanded"
  
  - name: "Vegetative"
    description: "Leaf and stem development phase"
    typicalDuration:
      value: 4
      unit: "weeks"
    environment:
      temperature:
        day:
          optimal: 24
          range:
            min: 20
            max: 28
        night:
          optimal: 20
          range:
            min: 18
            max: 24
      light:
        dailyDuration:
          hours: 18
        spectrum:
          primary: "blue"
          secondary: "red"
    nutrition:
      profile: "nitrogen-dominant"
      biologicalContext: "Supports vegetative growth"
    successCriteria:
      readinessForNextPhase: "When plant reaches 30-45cm with 6-8 nodes"
  
  - name: "Flowering"
    description: "Reproductive phase for flower development"
    typicalDuration:
      value: 8
      unit: "weeks"
    environment:
      light:
        dailyDuration:
          hours: 12
        spectrum:
          primary: "red"
          secondary: "blue"
      humidity:
        early:
          optimal: 50
          range:
            min: 40
            max: 60
        late:
          optimal: 40
          range:
            min: 35
            max: 45
        biologicalContext: "Lower humidity reduces mold risk"
    nutrition:
      profile: "phosphorus-potassium dominant"
      biologicalContext: "Supports flower development"
    successCriteria:
      harvestIndicators: ["80% darkened pistils", "milky trichomes"]

transitions:
  - from: "Vegetative"
    to: "Flowering"
    trigger:
      type: "time-based"
      condition: "after 4 weeks of vegetative growth"
    environmentalShift:
      light:
        dailyDuration:
          from: 18
          to: 12
          unit: "hours"
        transitionPeriod:
          value: 7
          unit: "days"
    biologicalContext: "Reducing light hours triggers flowering"

implementationGuidance:
  adaptationGuidelines:
    limitedCapabilities:
      noSpectrumControl: "Focus on light duration control"
```

## Conclusion

The revised OGSP Recipe Specification emphasizes a declarative approach to recipe definition, focusing on plant needs rather than implementation details. This approach makes recipes more portable across different growing systems and provides clearer guidance for growers.

By separating the "what" (plant needs) from the "how" (system implementation), the specification enables:

1. **Greater Recipe Portability**: Recipes can be used across diverse hardware systems
2. **Improved Knowledge Sharing**: Growers can share plant-centric knowledge without hardware dependencies
3. **Enhanced Adaptability**: Recipes can be adapted to different growing environments and resource constraints
4. **Better Educational Value**: Recipes provide biological context that helps growers understand plant needs
5. **Simplified Implementation**: Growing systems can interpret recipes according to their specific capabilities

This revision aligns with the OGSP's guiding principle of "Declarative Over Imperative" and supports the democratization of advanced growing techniques by making recipes more accessible and adaptable.
