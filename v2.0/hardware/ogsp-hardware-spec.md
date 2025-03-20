# OGSP Hardware Abstraction Specification (v2.0)

*This document is part of the OGSP 2.0 specification suite. For the overarching vision, motivation, and community-driven approach, please refer to the [Root Specification](../ogsp-root-spec.md).*

## Introduction
This document defines the standard interfaces and protocols for hardware abstraction within the OGSP protocol.

## Versioning
- Current Version: 2.0.0

## References
- [Root Specification](../ogsp-root-spec.md)
- [Core Protocol Specification](../core/ogsp-core-spec.md)
- [Recipe Representation Specification](../recipe/ogsp-recipe-spec.md)
- [Communication Protocol Specification](../communication/ogsp-communication-spec.md)
- [Security Specification](../security/ogsp-security-spec.md)

## Hardware Abstraction Layer

### Key Aspects
The Hardware Abstraction Layer (HAL) provides a standardized interface for sensors and actuators, allowing recipes to work across different hardware implementations. Key aspects include:
1. Device discovery and capability advertisement
2. Standardized command structures
3. Error handling and reporting
4. Calibration procedures
5. Maintenance status reporting
