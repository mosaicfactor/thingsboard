# ThingsBoard Project Structure

This document provides an overview of the ThingsBoard project's file structure and organization.

Created by [Juan Esteban Canelos](mailto:juan.canelos@mosaicfactor.com) with the help of Claude.

## Top-Level Directory Structure

```text
thingsboard/
├── application/        # Main ThingsBoard server application
├── common/             # Shared utilities and components
├── dao/                # Data Access Objects for database interactions
├── docker/             # Docker configurations for deployment
├── edqs/               # Entity Data Query Service
├── img/                # Static image assets
├── monitoring/         # System monitoring and observability components
├── msa/                # Microservices and monolithic deployment
├── netty-mqtt/         # Netty-based MQTT protocol implementation
├── packaging/          # Distribution packaging configurations
├── rest-client/        # Java client for ThingsBoard REST API
├── rule-engine/        # Rule engine for event processing
├── tools/              # Development and maintenance tools
├── transport/          # Protocol-specific transport implementations
└── ui-ngx/             # Angular-based web interface
```

## Core Components

### Application (`/application`)

The main ThingsBoard server Java application containing:

- Service implementations
- REST API controllers
- Security configurations
- Main application entry points

This module serves as the central component that ties together all other modules and provides the main executable application for ThingsBoard.

### Common (`/common`)

Shared components used across the platform that provide essential infrastructure:

- Actor system (`/common/actor`) - Actor-based architecture components for concurrent processing
- Data models (`/common/data`) - Entity models, DTOs, and core data structures
- Message queue (`/common/queue`) - Queue abstractions and implementations for asynchronous processing
- Utilities (`/common/util`) - Shared utility functions and helper classes

Additional components include:

- `/common/transport` - Common transport layer abstractions
- `/common/cache` - Caching mechanisms used throughout the platform
- `/common/message` - Message definitions for inter-component communication
- `/common/stats` - Statistics collection and management

This module forms the foundation for ThingsBoard's modular design, allowing consistent patterns and reusable components across the entire platform.

### Data Access Objects (`/dao`)

Database abstraction layer supporting different implementations:

- Entity DAO implementations
- SQL/NoSQL abstraction
- Time-series data management
- Cache implementations

This module provides a flexible data persistence layer that abstracts database operations from the business logic, allowing ThingsBoard to work with multiple database technologies.

### Docker (`/docker`)

Docker deployment configurations for different deployment scenarios, like:

**Docker Compose Files:**

- `/docker/docker-compose.yml` - Default composition for monolithic deployment
- `/docker/docker-compose-postgres.yml` - PostgreSQL-focused deployment with persistent volumes
- `/docker/docker-compose-cassandra.yml` - Setup with Cassandra for time-series data

**Component Configurations:**

- `/docker/tb-node` - ThingsBoard server node configuration
- `/docker/tb-transports` - Transport service configurations

This module provides ready-to-use container configurations that enable:

- Single-instance deployments for development
- Production-grade microservices deployments
- Hybrid database setups with separate persistence layers
- Scalable message broker integrations

The Docker configurations abstract the complexity of setting up the ThingsBoard environment, allowing users to quickly deploy the platform with different database backends and scaling options.

### Entity Data Query Service (`/edqs`)

A standalone microservice for efficient entity data querying:

- High-performance service for querying ThingsBoard entity data
- Implements gRPC interfaces for inter-service communication
- Optimized for complex entity data queries

This module provides specialized query capabilities that enhance ThingsBoard's ability to efficiently retrieve and process entity data.

### Monitoring (`/monitoring`)

System monitoring and observability components:

- Metrics collection and reporting
- Health check endpoints
- Performance monitoring dashboards
- Operational status indicators
- Integration with monitoring systems (Prometheus, Grafana)

This module provides capabilities for monitoring ThingsBoard's operational health, performance metrics, and system status, enabling administrators to ensure system reliability and quickly identify issues.

### Microservices and monolithic deployment (`/msa`)

This module orchestrates the packaging and Dockerization of ThingsBoard in both monolithic and microservices modes.

For monolithic deployments:

`/msa/tb`:

- Provides the build for the ThingsBoard single docker images.
- Generates the final `Dockerfile`, along with the necessary .sh, .xml, .conf, and .deb files.
- Supports PostgreSQL (`docker-postgres`) and hybrid PostgreSQL (entities) + Cassandra (timeseries) (`docker-cassandra`) setups.

This module enables ThingsBoard to be deployed in various configurations from single-node setups to highly available production clusters with independent scaling of different services.

### Netty MQTT (`/netty-mqtt`)

Custom MQTT protocol implementation based on Netty framework (a high-performance, non-blocking I/O framework for building networked applications in Java):

- High-performance MQTT broker functionality
- MQTT 3.1 and 5.0 protocol support
- QoS levels 0, 1, and 2 implementation
- Session management and persistence
- SSL/TLS support for secure communication

This module provides the foundational MQTT capabilities used by the ThingsBoard platform to handle device connectivity through the MQTT protocol.

### Packaging (`/packaging`)

Configuration and scripts for creating installable packages of ThingsBoard:

- Debian/Ubuntu package configurations
- RPM package configurations
- Windows service wrappers
- Distribution-specific configuration templates

This module handles the build processes required to package ThingsBoard into various distribution formats for easy installation on different operating systems and environments.

### REST Client (`/rest-client`)

Java client library for ThingsBoard REST API:

- High-level client for accessing ThingsBoard functionality programmatically
- Authentication and authorization handling
- Entity management operations
- Telemetry and attribute access
- Dashboard and widget manipulation

This module provides developers with a convenient way to integrate external applications with ThingsBoard using its REST API without having to handle the low-level HTTP communication details.

### Rule Engine (`/rule-engine`)

Event processing engine components that form ThingsBoard's business logic layer:

- Rule chain management for event processing workflows
- Node implementations for different functions:
  - Filters (message filtering based on conditions)
  - Transformers (data transformation and enrichment)
  - Actions (executing operations based on events)
- Integration nodes for external systems:
  - Email notifications
  - SMS messaging
  - Cloud service integrations (AWS, Azure, GCP)
  - External APIs
- Custom JavaScript execution nodes for flexible processing

Includes:

- `/rule-engine/rule-engine-api` - Core interfaces and abstractions
- `/rule-engine/rule-engine-components` - Standard rule node implementations

This module provides ThingsBoard's powerful event processing capabilities, allowing users to create complex automation workflows through a visual drag-and-drop interface without requiring programming skills. For advanced use cases, it supports custom JavaScript-based processing nodes.

### Tools (`/tools`)

A collection of separate utility applications that include migration, database operations and administrative utilities.

This module provides essential utilities that help with ThingsBoard maintenance, migration between versions, and system administration tasks, but are executed independently from the main application.

### Transport (`/transport`)

Protocol-specific implementations for device connectivity:

- CoAP - Constrained Application Protocol support for resource-constrained devices
- HTTP - HTTP protocol implementation for RESTful device APIs
- LwM2M - Lightweight M2M protocol support for device management
- MQTT - MQTT protocol implementation for pub/sub messaging
- SNMP - Simple Network Management Protocol support

This module enables ThingsBoard to communicate with diverse IoT devices using their native protocols, allowing for flexible deployment scenarios and broad device compatibility without requiring custom client-side code for standard IoT protocols.

### UI Components (`/ui-ngx`)

Angular-based web interface.

Key features include:

- Dashboard builder with drag-and-drop widgets
- Rule chain visual designer
- Device management interface
- Advanced widget library with customization options
- White-labeling and theming capabilities
- Role-based access control UI
- Responsive design for different devices
- Real-time data visualization components
- Support for multiple languages and internationalization

This module provides the end-user interface for ThingsBoard, allowing administrators, operators, and customers to interact with the platform through an intuitive web application. It leverages modern web technologies including Angular and Material Design components.
