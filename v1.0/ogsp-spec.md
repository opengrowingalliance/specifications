# RFC: Open Growing System Protocol (OGSP) Standard

**Version:** 1.0.0-draft  
**Date:** March 16, 2025  
**Status:** Proposed Standard  
**Authors:** Open Growing Alliance  

## Abstract

This RFC proposes the Open Growing System Protocol (OGSP), a standardized protocol for autonomous plant cultivation systems. OGSP enables interoperability between growing hardware, software, AI models, and recipe definitions, allowing for community-driven innovation while maintaining compatibility across implementations. This document establishes the core protocol specification, data formats, minimum implementation requirements, and extension mechanisms.

## Status of This Document

This document is a draft of a proposed industry standard. Distribution of this document is unlimited.

## Table of Contents

1. [Introduction](#1-introduction)
2. [Protocol Overview](#2-protocol-overview)
3. [Terminology](#3-terminology)
4. [Core Protocol Components](#4-core-protocol-components)
5. [Data Format and Schema](#5-data-format-and-schema)
6. [Recipe Structure](#6-recipe-structure)
7. [Communication Standards](#7-communication-standards)
8. [Compatibility and Versioning](#8-compatibility-and-versioning)
9. [Security Considerations](#9-security-considerations)
10. [Minimum Implementation Requirements](#10-minimum-implementation-requirements)
11. [Extension Mechanisms](#11-extension-mechanisms)
12. [Conformance Testing](#12-conformance-testing)
13. [Governance and Evolution](#13-governance-and-evolution)
14. [References](#14-references)
15. [Appendices](#15-appendices)

## 1. Introduction

### 1.1 Motivation

Current growing systems operate as closed ecosystems, preventing interoperability between hardware components, software controllers, and growing methodologies. This creates vendor lock-in, inhibits innovation, and blocks knowledge-sharing within the growing community. The Open Growing System Protocol (OGSP) aims to solve these challenges by providing a standardized way for different components to communicate and collaborate.

### 1.2 Design Goals

The OGSP aims to:

1. Enable recipe portability across compatible hardware systems
2. Create a vibrant ecosystem of interoperable sensors, actuators, and AI models
3. Facilitate community sharing and improvement of growing methodologies
4. Support progression from manual to assisted to fully autonomous growing
5. Establish clear versioning and backward compatibility guidelines
6. Enable hardware-agnostic recipe development and optimization
7. Provide secure and private sharing mechanisms
8. Support a wide range of plant types and growing methodologies

### 1.3 Use Cases

The OGSP supports the following primary use cases:

1. **Recipe Development and Sharing**: Growers creating, forking, and sharing optimized growing recipes
2. **Hardware Interoperability**: Components from different manufacturers working together
3. **DIY and Commercial Growing**: Supporting both hobbyist and commercial cultivation systems
4. **AI/ML Integration**: Standardized interfaces for AI-enhanced growing assistance
5. **Data Collection and Analysis**: Uniform formats for collecting, analyzing and leveraging growing data
6. **Emergency Handling**: Standard protocols for system failures and environmental emergencies

## 2. Protocol Overview

The OGSP consists of several interconnected components:

1. **Recipe Definition Language**: A declarative YAML-based format describing complete growing instructions
2. **Hardware Abstraction Layer**: Standardized interfaces for sensors and actuators
3. **Communication Protocols**: Standards for system component communication
4. **AI/ML Integration Specification**: Methods for utilizing AI capabilities across the system
5. **Data Collection Standards**: Formats for storing historical grow data
6. **Version Control Integration**: Mechanisms for recipe evolution and sharing

The protocol follows these key design principles:

1. **Declarative Over Imperative**: Recipes describe what to achieve, not how to achieve it
2. **Progressive Enhancement**: Basic functionality without advanced capabilities, enhanced when available
3. **Graceful Degradation**: Systems should function reasonably even when components are missing
4. **Security by Design**: Authentication, encryption, and permission controls built-in
5. **Extensibility**: Mechanisms for adding new capabilities without breaking existing implementations

## 3. Terminology

- **Recipe**: A complete set of instructions for growing a specific plant from start to finish
- **Phase**: A distinct stage in a plant's growth cycle with specific environmental requirements
- **Sensor**: Any device that measures environmental or plant conditions
- **Actuator**: Any device that can modify the growing environment
- **AI Sensor**: Virtual sensors that derive higher-level insights from raw sensor data
- **Controller**: The system component that orchestrates sensors and actuators according to the recipe
- **Parameter**: A specific environmental condition (temperature, humidity, etc.)
- **Automation Rule**: A condition-action pair that triggers automated responses
- **Confidence Score**: A value indicating AI model certainty about a detection or recommendation
- **Growing System**: The complete collection of hardware and software running the OGSP

## 4. Core Protocol Components

### 4.1 Recipe Protocol

The Recipe Protocol defines the structure and semantics of growing recipes. It includes:

1. Metadata and version information
2. Environmental requirements
3. Phase definitions with transitions
4. Monitoring and alert configurations
5. Hardware requirements
6. Automation rules
7. AI integration specifications
8. Emergency protocols

### 4.2 Hardware Abstraction Layer

The Hardware Abstraction Layer (HAL) provides a standardized interface for sensors and actuators, allowing recipes to work across different hardware implementations. Key aspects include:

1. Device discovery and capability advertisement
2. Standardized command structures
3. Error handling and reporting
4. Calibration procedures
5. Maintenance status reporting

### 4.3 Communication Layer

The Communication Layer defines how components in a growing system communicate, supporting:

1. Local communications (within a single system)
2. Remote management protocols
3. Cloud integration standards
4. Peer-to-peer recipe sharing
5. Real-time data streaming
6. Batch data operations

### 4.4 AI Integration Framework

The AI Integration Framework standardizes how AI capabilities are incorporated:

1. AI model specification and versioning
2. Input/output formats for models
3. Confidence score reporting
4. Extensibility for new AI capabilities
5. Training data formats and handling
6. Explainability requirements
7. Multi-agent coordination standards

## 5. Data Format and Schema

### 5.1 Primary Data Format

YAML is the primary data format for OGSP recipes, chosen for:

1. Human readability and editability
2. Compatibility with version control systems
3. Support for comments and documentation
4. Wide language and tool support
5. Schema validation capabilities

All OGSP-compliant systems MUST support YAML 1.2 or later for recipe parsing.

### 5.2 Schema Definition

The OGSP schema is defined using JSON Schema (Draft 2020-12) and is available at `https://opengrowingtrust.org/schema/ogsp/1.0/`.

Systems MUST validate recipes against this schema before execution. Implementation errors MUST be clearly reported with line numbers and explanations.

### 5.3 Additional Representation Formats

While YAML is the canonical format, systems MAY also support:

1. JSON for programmatic interfaces
2. XML for enterprise integrations
3. Binary formats for resource-constrained environments

Conversion between formats MUST preserve all data and semantics.

## 6. Recipe Structure

### 6.1 Recipe Components

A complete OGSP recipe consists of the following components:

1. **Metadata**: Basic information about the recipe
2. **Environment**: Requirements for the growing environment
3. **Phases**: Detailed instructions for each growth phase
4. **Sensors**: Required and optional sensing capabilities
5. **Actuators**: Required and optional actuation capabilities
6. **Automation Rules**: Event-response pairs for autonomous operation
7. **Data Collection**: Specifications for data gathering and storage
8. **AI/ML Capabilities**: Required AI models and capabilities
9. **Emergency Protocols**: Procedures for handling system failures
10. **Integrations**: External system connectivity requirements
11. **Version Control**: Recipe tracking and evolution information

### 6.2 Recipe Versioning

Recipes MUST include semantic versioning (MAJOR.MINOR.PATCH) following these rules:

1. MAJOR version changes when incompatible changes are made
2. MINOR version changes when functionality is added in a backward-compatible manner
3. PATCH version changes when backward-compatible bug fixes are implemented

Systems MUST check version compatibility before execution.

### 6.3 Recipe Validation

Growing systems MUST validate recipes before execution, checking:

1. Schema conformance
2. Internal consistency
3. Hardware compatibility
4. Safety parameters
5. Resource requirements

Validation failures MUST be reported with clear error messages indicating the specific issue and its location within the recipe.

## 7. Communication Standards

### 7.1 Local Communication

Components within a single growing system MUST support at least one of:

1. MQTT 5.0 for event-based communication
2. HTTP/2 RESTful APIs for request-response patterns
3. WebSockets for bidirectional communication

Local communication SHOULD use TLS 1.3 or later for encryption, even within trusted networks.

### 7.2 Remote Management

Systems exposing remote management capabilities MUST implement:

1. HTTPS with TLS 1.3 or later
2. OAuth 2.0 or OpenID Connect for authentication
3. Role-based access control
4. Rate limiting and brute force protection
5. Audit logging of all management actions

### 7.3 Data Streaming

For real-time data streaming, systems MUST support:

1. Server-Sent Events or WebSockets for web clients
2. MQTT for IoT integrations
3. gRPC for high-performance programmatic access

Stream formats MUST be documented using OpenAPI 3.1 or AsyncAPI 2.0 specifications.

### 7.4 Discovery Protocol

Growing systems MUST implement a discovery protocol enabling:

1. Automatic detection of sensors and actuators
2. Capability advertisements
3. Network topology discovery
4. Controller election in multi-controller setups
5. Service advertisement

The discovery protocol SHOULD use mDNS/DNS-SD for local network discovery and a registry system for cloud-based discovery.

## 8. Compatibility and Versioning

### 8.1 Protocol Versioning

The OGSP uses semantic versioning (MAJOR.MINOR.PATCH) with these guarantees:

1. MAJOR version increases with backward-incompatible changes
2. MINOR version increases with added functionality maintaining backward compatibility
3. PATCH version increases with backward-compatible bug fixes

### 8.2 Backward Compatibility

Systems supporting OGSP 1.x MUST:

1. Accept valid recipes from any 1.y version where y ≤ x
2. Ignore unknown fields in recipes from future MINOR versions
3. Reject recipes requiring features from future MAJOR versions
4. Provide clear error messages when rejecting incompatible recipes

### 8.3 Feature Detection

Growing systems MUST implement feature detection allowing:

1. Recipes to adapt to available capabilities
2. Graceful degradation when optional features are unavailable
3. Progressive enhancement when advanced features are available

Feature detection follows the capability advertisement pattern using the standard HAL interface.

### 8.4 Deprecation Policy

Protocol features MAY be deprecated following these rules:

1. Features MUST be marked deprecated for one full MINOR version cycle before removal
2. Deprecation notices MUST include migration paths
3. Deprecated features MUST continue functioning until removed in a MAJOR version
4. Documentation MUST clearly indicate deprecated status

## 9. Security Considerations

### 9.1 Authentication and Authorization

Growing systems MUST implement:

1. Strong authentication for all management interfaces
2. Role-based access control with principle of least privilege
3. Secure credential storage with no plaintext passwords
4. Session management with secure timeout policies
5. Multi-factor authentication for critical operations

### 9.2 Data Protection

All sensitive data MUST be protected:

1. TLS 1.3 or later for data in transit
2. AES-256 or equivalent for data at rest
3. Key rotation policies
4. Secure key management
5. Data minimization practices

### 9.3 Recipe Integrity

Recipe integrity MUST be maintained:

1. Digital signatures for shared recipes
2. Tamper detection mechanisms
3. Version history preservation
4. Audit trails for changes
5. Chain of custody tracking

### 9.4 Privacy Considerations

Systems MUST respect user privacy:

1. Clear data collection notices
2. Opt-in for telemetry and community sharing
3. Anonymization of shared data
4. Data portability mechanisms
5. Right to deletion capabilities

### 9.5 Secure Defaults

All implementations MUST use secure defaults:

1. Encryption enabled by default
2. Restrictive permissions by default
3. Minimal network exposure
4. Automatic security updates
5. Fail-secure error handling

## 10. Minimum Implementation Requirements

### 10.1 Core Protocol Support

A compliant OGSP implementation MUST support:

1. Complete recipe parsing and validation
2. Basic phase execution with transitions
3. Sensor and actuator abstraction
4. Simple automation rules
5. Local data storage
6. Emergency handling for power and connectivity failures

### 10.2 Minimal Hardware Requirements

At minimum, a compliant system MUST support:

1. Temperature sensing
2. Humidity sensing
3. Light control (on/off and scheduling)
4. Basic notification mechanism

### 10.3 Progressive Capability Levels

The OGSP defines four capability levels:

1. **Level 1 (Basic)**: Manual operation with recipe guidance
2. **Level 2 (Assisted)**: Basic automation of environmental controls
3. **Level 3 (Autonomous)**: Full automation with minimal intervention
4. **Level 4 (Intelligent)**: AI-driven optimization and adaptation

Systems MUST advertise their capability level and gracefully handle recipes requiring higher levels.

## 11. Extension Mechanisms

### 11.1 Vendor Extensions

Vendors MAY extend the protocol using the following namespace pattern:

```yaml
x-vendor-feature:
  property1: value1
  property2: value2
```

Systems MUST ignore unknown extensions but MAY provide warnings about them.

### 11.2 Standardized Extensions

Common extensions MAY be standardized through the OGSP Extension Process:

1. Proposal submission to the OGSP Working Group
2. Review and feedback period
3. Reference implementation requirement
4. Formal specification publication
5. Extension registry inclusion

Standardized extensions use the namespace pattern:

```yaml
ext-name:
  specification: "https://opengrowingtrust.org/extensions/name/1.0/"
  # Extension properties
```

### 11.3 AI Model Extensions

AI model extensions follow a specialized pattern:

```yaml
ai-model:
  type: "plant_health_analyzer"
  version: ">=2.0.0"
  capabilities:
    - "disease_detection"
    - "nutrient_deficiency_analysis"
  fallback_behavior: "use_standard_thresholds"
```

Systems MUST handle missing AI capabilities gracefully through specified fallback behaviors.

## 12. Conformance Testing

### 12.1 Validation Suite

A standard validation suite is available at `https://opengrowingtrust.org/validation/` including:

1. Schema validation tools
2. Reference recipes for testing
3. Communication protocol test suite
4. Security assessment tools
5. Performance benchmarks

Systems claiming OGSP compliance MUST pass all relevant validation tests.

### 12.2 Certification Process

The Open Growing Alliance offers certification through:

1. Self-certification with published results
2. Third-party validation for formal certification
3. Compatibility badge program

Certified systems are listed in the public registry at `https://opengrowingtrust.org/certified/`.

### 12.3 Reference Implementation

A reference implementation is maintained at `https://github.com/opengrowingtrust/reference-ogsp` providing:

1. Recipe parser and validator
2. Simulator for testing
3. Sample hardware implementations
4. Documentation and examples
5. Development tools

The reference implementation is licensed under Apache 2.0.

## 13. Governance and Evolution

### 13.1 Working Group Structure

The OGSP is governed by:

1. **Core Working Group**: Responsible for protocol specification
2. **Extension Working Group**: Handles extension proposals
3. **Security Working Group**: Focuses on security aspects
4. **Community Working Group**: Manages adoption and outreach

Working groups operate under a meritocratic governance model with transparent decision-making.

### 13.2 Specification Process

Protocol evolution follows:

1. Issue identification and discussion
2. Proposal submission with rationale
3. Public comment period (minimum 60 days)
4. Implementation in reference code
5. Final specification publication

All discussions and decisions are publicly documented.

### 13.3 Version Lifecycle

Each MAJOR version has a defined lifecycle:

1. **Draft**: Initial proposal
2. **Proposed Standard**: Stable for implementation
3. **Standard**: Widely implemented with proven interoperability
4. **Legacy**: Superseded by newer versions but still supported
5. **Historic**: No longer supported

MAJOR versions receive security updates for a minimum of 5 years after reaching Legacy status.

## 14. References

### 14.1 Normative References

1. YAML 1.2 Specification, https://yaml.org/spec/1.2/spec.html
2. JSON Schema Draft 2020-12, https://json-schema.org/specification.html
3. Semantic Versioning 2.0.0, https://semver.org/
4. RFC 7519: JSON Web Token (JWT), https://tools.ietf.org/html/rfc7519
5. RFC 8446: TLS 1.3, https://tools.ietf.org/html/rfc8446

### 14.2 Informative References

1. Open Agriculture Foundation, "Food Computer Documentation"
2. Plant Phenotyping and Imaging Research Centre, "Data Standards for Plant Phenotyping"
3. W3C Web of Things (WoT) Architecture, https://www.w3.org/TR/wot-architecture/
4. Open Source Ecology, "Open Hardware Documentation Standard"

## 15. Appendices

### Appendix A: Example Minimal Recipe

```yaml
metadata:
  name: "Basic Tomato Grow"
  version: "1.0.0"
  author: "Open Growing Alliance"
  description: "Simple tomato growing recipe for demonstration"
  
environment:
  ambient_conditions:
    temperature_range_c: [18, 28]
    humidity_range_percent: [40, 70]
    
phases:
  - name: "seedling"
    duration: "14 days"
    conditions:
      light:
        cycle: "16/8"  # hours on/off
      water:
        schedule: "every_2_days"
    transition_triggers:
