# Video Streaming Platform (VSP)

![Java](https://img.shields.io/badge/Java-21-007396?logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4.5-6DB33F?logo=springboot&logoColor=white)
![Spring Cloud](https://img.shields.io/badge/Spring%20Cloud-2024.0.0-2C6EBE?logo=spring&logoColor=white)
![Gradle](https://img.shields.io/badge/Gradle-8.14-4B6587?logo=gradle&logoColor=white)
![Status](https://img.shields.io/badge/status-in_progress-F5C910?label=Status)


This repository serves as the **central hub** for the **Video Streaming Platform (VSP)**, a cloud-native, microservices-based application designed to deliver a scalable, reliable and high-performance video streaming experience.

It provides an overview of the system architecture and links to all individual microservices, acting as the single entry point for developers, maintainers and reviewers.


## Table of Contents

* [Introduction](#introduction)
* [High-Level Architecture](#high-level-architecture)
* [Microservices](#microservices)
  * [Statuses](#statuses)
  * [Frontend Apps](#frontend-apps)
  * [Infrastructure Services](#infrastructure-services)
  * [Core Backend Services](#core-backend-services)
    * [Auth Cluster](#auth-cluster)
    * [Users Cluster](#users-cluster)
    * [Media Cluster](#media-cluster)
    * [Streaming Cluster](#streaming-cluster)
    * [Discovery Cluster](#discovery-cluster)
  * [Supporting Backend Services](#supporting-backend-services)
    * [Engagement Cluster](#engagement-cluster)
    * [Comms Cluster](#comms-cluster)
    * [Billing Cluster](#billing-cluster)
    * [Analytics Cluster](#analytics-cluster)
    * [Support Cluster](#support-cluster)
* [Technology Stack](#technology-stack)
  * [Frontend](#frontend)
  * [Backend](#backend)
  * [Infrastructure](#infrastructure)
  * [Service Communication](#service-communication)
* [Deployment](#deployment)
  * [Prerequisites](#prerequisites)
  * [Deployment Process](#deployment-process)
  * [CI/CD](#cicd)
* [License](#license)
* [Contact](#contact)


## Introduction

The **Video Streaming Platform** is a modern, cloud-native solution that leverages a microservices architecture to deliver a scalable and high-performance streaming experience. Designed for flexibility and resilience, it divides key functionalities into dedicated services, including user management, media catalog, streaming, search, recommendations, authentication and more.

Key features of the platform include:
- **Microservices-based architecture**: Each core function is implemented as an independent service, promoting modularity, maintainability and scalability.
- **Cloud-native deployment**: Utilises containerisation and orchestration to support dynamic scaling and high availability.
- **Robust communication**: Integrates REST, gRPC and asynchronous messaging to ensure efficient and reliable inter-service communication.
- **Centralised configuration and service discovery**: Leverages Spring Cloud Config and Eureka for streamlined configuration management and dynamic service registration.

This hub repository is the starting point for understanding, deploying and maintaining the entire platform. It provides architecture diagrams, technology stack information and direct links to each microservice repository to ensure that developers and stakeholders can easily navigate and contribute to the system.


## High-Level Architecture

The platform is built on a modern, cloud-native architecture that divides key platform functionalities into dedicated microservices, each deployed within its own cluster. This modular approach allows each service to scale independently, ensures high availability, and enables rapid feature development and deployment.

The high-level architecture diagram below illustrates how frontend clients interact with the platform's core infrastructure and service clusters. Each cluster contains independent microservices with their own dedicated databases, ensuring data consistency and service autonomy.

<p align="center">
  <img src="docs/diagrams/architecture-diagram.png" alt="VSP High-Level Architecture" style="max-width: 800px; width: 100%; height: auto;"/>
</p>

At the heart of the architecture is the **API Gateway**, which serves as the single entry point for all client requests. It provides routing, authentication, rate-limiting and request aggregation, simplifying client interactions while abstracting the complexity of the underlying microservices.

Microservices are organised into logical clusters based on their core responsibilities. Inter-service communication uses a combination of **REST**, **gRPC** and asynchronous messaging (**Kafka**, **RabbitMQ**), ensuring efficient and reliable data exchange even under high load.

Centralised configuration management is provided via **Spring Cloud Config**, enabling consistent, environment-specific configuration across all microservices. **Eureka** acts as the service registry, supporting dynamic service discovery and load balancing.


## Microservices

This section outlines the core components of **VSP**, their current development statuses, and links to individual repositories where applicable.


### Statuses

- **Planned**: Service is scheduled for future development.
- **Pending**: Service is under consideration but not yet prioritised.
- **Concept Only**: Service is a conceptual idea that may be explored in the future.


### Frontend Apps

User-facing applications delivering the video streaming experience across web, mobile and smart TVs.

<table style="width: 100%">
  <tr style="vertical-align: top;">
    <th style="width: 25%;">Service Name</th>
    <th style="width: 50%;">Description</th>
    <th style="width: 25%;">Repository / Status</th>
  </tr>
  <tr style="vertical-align: top;">
    <td>Web App</td>
    <td>Provides the main user interface for desktop and laptop users, supporting media browsing, playback and account management.</td>
    <td><code>Planned</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Mobile App</td>
    <td>Delivers the platform experience to iOS and Android users, including video playback, offline support and push notifications.</td>
    <td><code>Concept Only</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>TV App</td>
    <td>Designed for smart TVs and streaming devices, offering a lean-back experience optimised for large screens and remote controls.</td>
    <td><code>Concept Only</code></td>
  </tr>
</table>


### Infrastructure Services

Essential infrastructure services, including configuration management, service discovery and API routing.

<table style="width: 100%">
  <tr style="vertical-align: top;">
    <th style="width: 25%;">Service Name</th>
    <th style="width: 50%;">Description</th>
    <th style="width: 25%;">Repository / Status</th>
  </tr>
  <tr style="vertical-align: top;">
    <td>Config Server</td>
    <td>Manages externalised configuration for all services using Spring Cloud Config, enabling dynamic configuration updates and environment-specific settings.</td>
    <td><a href="https://github.com/mzilin/vsp-infra-config">vsp-infra-config</a></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Discovery Service</td>
    <td>Provides dynamic service registration and discovery using Spring Cloud Netflix Eureka, enabling microservices to locate and communicate with each other seamlessly.</td>
    <td><a href="https://github.com/mzilin/vsp-infra-discovery">vsp-infra-discovery</a></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>API Gateway</td>
    <td>Routes external client requests to the appropriate microservices using Spring Cloud Gateway, handling authentication, rate limiting and request aggregation.</td>
    <td><a href="https://github.com/mzilin/vsp-infra-gateway">vsp-infra-gateway</a></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Chaos Monkey</td>
    <td>Injects faults and simulates failures in services using Spring Cloud Chaos Monkey, helping to test the platform's resilience and fault tolerance.</td>
    <td><code>Pending</code></td>
  </tr>
</table>


### Core Backend Services

The backend microservices that power the platform, grouped by functional cluster for easy navigation.


#### Auth Cluster

Manages user authentication, session control and third-party login integrations.

<table style="width: 100%" >
  <tr style="vertical-align: top;">
    <th style="width: 25%;">Service Name</th>
    <th style="width: 50%;">Description</th>
    <th style="width: 25%;">Repository / Status</th>
  </tr>
  <tr style="vertical-align: top;">
    <td>Identity Service</td>
    <td>Handles user authentication, storing and verifying credentials securely.</td>
    <td><a href="https://github.com/mzilin/vsp-auth-identity">vsp-auth-identity</a></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Session Service</td>
    <td>Controls access and refresh tokens, including validation, rotation and token blacklisting.</td>
    <td><a href="https://github.com/mzilin/vsp-auth-session">vsp-auth-session</a></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>OAuth2 Service</td>
    <td>Supports third-party login integrations, managing linked identities.</td>
    <td><code>Concept Only</code></td>
  </tr>
</table>


#### Users Cluster

Handles user-related data such as account details, profiles, watchlists and device management.

<table style="width: 100%" >
  <tr style="vertical-align: top;">
    <th style="width: 25%;">Service Name</th>
    <th style="width: 50%;">Description</th>
    <th style="width: 25%;">Repository / Status</th>
  </tr>
  <tr style="vertical-align: top;">
    <td>Account</td>
    <td>Stores and manages core user account information.</td>
    <td><a href="https://github.com/mzilin/vsp-users-account">vsp-users-account</a></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Profile</td>
    <td>Manages user profiles, preferences and personalisation settings.</td>
    <td><a href="https://github.com/mzilin/vsp-users-profile">vsp-users-profile</a></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Watchlist</td>
    <td>Allows users to save and manage a list of shows and films to watch later.</td>
    <td><code>Pending</code></td>
  </tr>
    <tr style="vertical-align: top;">
    <td>Devices</td>
    <td>Tracks registered user devices and session history (e.g. IP, location, timestamps).</td>
    <td><code>Concept Only</code></td>
  </tr>
</table>


#### Media Cluster

Manages media content, including uploads, transcoding, DRM and licensing.

<table style="width: 100%">
  <tr style="vertical-align: top;">
    <th style="width: 25%;">Service Name</th>
    <th style="width: 50%;">Description</th>
    <th style="width: 25%;">Repository / Status</th>
  </tr>
  <tr style="vertical-align: top;">
    <td>Catalog</td>
    <td>Stores metadata for all media, including titles, genres, trailers and cast details.</td>
    <td><a href="https://github.com/mzilin/vsp-media-catalog">vsp-media-catalog</a></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Upload</td>
    <td>Handles media uploads to S3 for further processing and storage.</td>
    <td><code>Planned</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Transcoder</td>
    <td>Converts media into different formats for streaming.</td>
    <td><code>Planned</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>DRM (Digital Rights Management)</td>
    <td>Protects content with encryption and controls playback rights.</td>
    <td><code>Concept Only</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Geo-Restrictions Manager</td>
    <td>Restricts content availability based on geographic location.</td>
    <td><code>Concept Only</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Content Moderation</td>
    <td>Ensures uploaded content meets community and legal standards.</td>
    <td><code>Concept Only</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Release Scheduler</td>
    <td>Controls when content is published and for how long it's available.</td>
    <td><code>Concept Only</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Licensing Service</td>
    <td>Manages content licensing agreements and rights.</td>
    <td><code>Concept Only</code></td>
  </tr>
</table>


#### Streaming Cluster

Delivers streaming services, including content delivery, playback management and CDN integration.

<table style="width: 100%">
  <tr style="vertical-align: top;">
    <th style="width: 25%;">Service Name</th>
    <th style="width: 50%;">Description</th>
    <th style="width: 25%;">Repository / Status</th>
  </tr>
  <tr style="vertical-align: top;">
    <td>Delivery</td>
    <td>Streams content to users using a CDN for high performance and scale.</td>
    <td><code>Planned</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Playback Context</td>
    <td>Builds real-time playback sessions, including entitlements and resume data.</td>
    <td><code>Planned</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Rights Manager</td>
    <td>Validates user permissions for content based on subscriptions, geo and device.</td>
    <td><code>Concept Only</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Watch History</td>
    <td>Stores user watch history, timestamps and resume points.</td>
    <td><code>Planned</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>CDN Orchestrator</td>
    <td>Selects the best CDN edge node for each user, integrating with Open Connect.</td>
    <td><code>Concept Only</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Live</td>
    <td>Handles live streaming events and real-time playback.</td>
    <td><code>Concept Only</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Ad Inserter</td>
    <td>Injects or signals ad content into live or on-demand streams.</td>
    <td><code>Concept Only</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Offline Manager</td>
    <td>Manages downloads, licenses and expiry for offline viewing.</td>
    <td><code>Concept Only</code></td>
  </tr>
</table>


#### Discovery Cluster

Provides search and discovery features, including search indexing, autocomplete and homepage content curation.

<table style="width: 100%">
  <tr style="vertical-align: top;">
    <th style="width: 25%;">Service Name</th>
    <th style="width: 50%;">Description</th>
    <th style="width: 25%;">Repository / Status</th>
  </tr>
  <tr style="vertical-align: top;">
    <td>Search</td>
    <td>Provides full-text and filtered search on media catalogues.</td>
    <td><a href="https://github.com/mzilin/vsp-discovery-search">vsp-discovery-search</a></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Autocomplete</td>
    <td>Suggests search terms and titles as users type.</td>
    <td><code>Pending</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Homepage Engine</td>
    <td>Builds personalised content rows for users by combining recommendations, trending titles and viewing history.</td>
    <td><code>Pending</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Catalogue Indexer</td>
    <td>Keeps Elasticsearch in sync with the media catalogue for fast search results.</td>
    <td><code>Planned</code></td>
  </tr>
</table>


### Supporting Backend Services

Provides key platform enhancements such as user engagement, recommendations, communication, billing, analytics and support.


#### Engagement Cluster

Drives user interaction with recommendations, trending content, A/B testing and advertising.

<table style="width: 100%" >
  <tr style="vertical-align: top;">
    <th style="width: 25%;">Service Name</th>
    <th style="width: 50%;">Description</th>
    <th style="width: 25%;">Repository / Status</th>
  </tr>
  <tr style="vertical-align: top;">
    <td>Recommender</td>
    <td>Uses machine learning to suggest content based on user behaviour and history.</td>
    <td><code>Pending</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Trending</td>
    <td>Identifies and displays currently popular shows and films.</td>
    <td><code>Pending</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>A/B Testing</td>
    <td>Runs experiments to test new features and content layouts.</td>
    <td><code>Concept Only</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Ads</td>
    <td>Manages ad campaigns, targeting, scheduling and selection for live streams.</td>
    <td><code>Concept Only</code></td>
  </tr>
</table>


#### Comms Cluster

Manages user communication via email, push notifications, in-app messages and user preferences.

<table style="width: 100%">
  <tr style="vertical-align: top;">
    <th style="width: 25%;">Service Name</th>
    <th style="width: 50%;">Description</th>
    <th style="width: 25%;">Repository / Status</th>
  </tr>
  <tr style="vertical-align: top;">
    <td>Notification Orchestrator</td>
    <td>Routes and schedules messages across multiple channels.</td>
    <td><code>Pending</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Email</td>
    <td>Sends transactional and marketing emails.</td>
    <td><a href="https://github.com/mzilin/vsp-comms-email">vsp-comms-email</a></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Push (Apps)</td>
    <td>Sends push notifications to mobile devices.</td>
    <td><code>Concept Only</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>In-App (Websockets)</td>
    <td>Delivers real-time messages within web and mobile apps via WebSockets.</td>
    <td><code>Planned</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>SMS</td>
    <td>Sends text messages via telecom providers.</td>
    <td><code>Concept Only</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Templates</td>
    <td>Manages message templates for consistent formatting.</td>
    <td><code>Concept Only</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Preferences</td>
    <td>Handles user communication preferences and settings.</td>
    <td><code>Concept Only</code></td>
  </tr>
</table>


#### Billing Cluster

Handles payments, subscriptions, refunds and financial reconciliation.

<table style="width: 100%" >
  <tr style="vertical-align: top;">
    <th style="width: 25%;">Service Name</th>
    <th style="width: 50%;">Description</th>
    <th style="width: 25%;">Repository / Status</th>
  </tr>
  <tr style="vertical-align: top;">
    <td>Payments</td>
    <td>Processes payments using Stripe/Checkout/etc.</td>
    <td><code>Pending</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Invoicing</td>
    <td>Generates and stores user invoices.</td>
    <td><code>Concept Only</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Subscriptions</td>
    <td>Manages plans, renewals and subscription statuses.</td>
    <td><code>Pending</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Refunds</td>
    <td>Processes user refund requests and tracks their status.</td>
    <td><code>Concept Only</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Disputes</td>
    <td>Handles chargebacks and interactions with payment providers.</td>
    <td><code>Concept Only</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Reconciliation</td>
    <td>Compares internal records with provider statements to identify mismatches.</td>
    <td><code>Concept Only</code></td>
  </tr>
</table>


#### Analytics Cluster

Enables platform insights by collecting, analysing, and reporting data on content and user behaviour.

<table style="width: 100%" >
  <tr style="vertical-align: top;">
    <th style="width: 25%;">Service Name</th>
    <th style="width: 50%;">Description</th>
    <th style="width: 25%;">Repository / Status</th>
  </tr>
  <tr style="vertical-align: top;">
    <td>Event Collector</td>
    <td>Ingests and batches user and system events.</td>
    <td>Concept Only</a></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Reporting</td>
    <td>Generates dashboards and usage statistics.</td>
    <td><code>Concept Only</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Content Performance</td>
    <td>Tracks views, engagement and popularity of titles.</td>
    <td>Concept Only</a></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>User Behaviour</td>
    <td>Stores behaviour data for analysis and machine learning.</td>
    <td><code>Concept Only</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Anomaly Detector</td>
    <td>Detects spikes, drops or odd patterns in metrics in real-time.</td>
    <td><code>Concept Only</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Data Quality Validator</td>
    <td>Monitors pipelines for broken schemas and missing data.</td>
    <td><code>Concept Only</code></td>
  </tr>
  <tr style="vertical-align: top;">
    <td>Ad Metrics</td>
    <td>Tracks ad impressions, durations, aggregates revenue/performance data.</td>
    <td><code>Concept Only</code></td>
  </tr>
</table>


#### Support Cluster

Manages customer support, including ticketing and helpdesk integrations.

<table style="width: 100%" >
  <tr style="vertical-align: top;">
    <th style="width: 25%;">Service Name</th>
    <th style="width: 50%;">Description</th>
    <th style="width: 25%;">Repository / Status</th>
  </tr>
  <tr style="vertical-align: top;">
    <td>Ticketing</td>
    <td>Handles customer support tickets and related workflows.</td>
    <td>Concept Only</a></td>
  </tr>
</table>


## Technology Stack

![React](https://img.shields.io/badge/React-20232A?logo=react&logoColor=61DAFB&style=flat)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-6DB33F?logo=springboot&logoColor=white)
![Eureka](https://img.shields.io/badge/Eureka-2C6EBE?logo=spring&logoColor=white)
![Apache Kafka](https://img.shields.io/badge/Kafka-231F20?logo=apachekafka&logoColor=white)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-FF6600?logo=rabbitmq&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?logo=redis&logoColor=white)
![Cassandra](https://img.shields.io/badge/Cassandra-1287B1?logo=apachecassandra&logoColor=white)
![DynamoDB](https://img.shields.io/badge/DynamoDB-4053D6?logo=amazon-dynamodb&logoColor=white)
![ClickHouse](https://img.shields.io/badge/ClickHouse-F5C910?logo=clickhouse&logoColor=black)
![Elasticsearch](https://img.shields.io/badge/Elasticsearch-005571?logo=elasticsearch&logoColor=white)
![BigQuery](https://img.shields.io/badge/BigQuery-3367D6?logo=googlebigquery&logoColor=white)
![Amazon S3](https://img.shields.io/badge/S3-569A31?logo=amazonwebservices&logoColor=white)
![Amazon CloudFront](https://img.shields.io/badge/CloudFront-232F3E?logo=amazonwebservices&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?logo=grafana&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?logo=prometheus&logoColor=white)


### Frontend
- Built as a **React** single-page application (SPA)
- Communicates with the backend via the **API Gateway**
- Uses **HTTP-only JWT** cookies for authentication


### Backend
- Microservices architecture with services grouped by business domain
- **Spring Boot** for core business services
- **Spring Cloud** provides service discovery, configuration and gateway routing
- Polyglot persistence: each service owns its own database


### Infrastructure
- Containerised deployments using **AWS ECS Fargate**
- CI/CD pipeline using **GitHub Actions** for automated builds and deployments
- Monitoring and observability with **Prometheus** and **Grafana**


### Service Communication
- Services communicate using **REST**, **gRPC** and messaging systems (**RabbitMQ**, **Kafka**) depending on the use case and performance needs.


## Deployment

Each microservice in this platform is designed to be containerised and deployed consistently using Docker, with CI/CD pipelines for automated builds, tests and deployments.


### Prerequisites

Ensure you have the following installed on your machine:
- [Java JDK 21](https://www.oracle.com/uk/java/technologies/downloads/#java21)
- [Gradle 8.14](https://gradle.org/)
- [Docker](https://docs.docker.com/get-started/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/)

### Deployment Process

Each microservice follows a similar deployment process:
1.	**Build**: The project is containerised using Docker and tagged with a version.
2.	**Push**: The built image is pushed to the **AWS ECR** container registry.
3.	**Deploy**: The image is pulled from the registry and deployed to the **AWS ECS** environment.
4.	**Monitor**: Logs and metrics are collected for operational monitoring.

### CI/CD

- **Continuous Integration**: All commits to key branches trigger automated build and test pipelines to ensure code quality.
- **Continuous Deployment**: When changes are merged into the `prod` branch, a deploy pipeline is triggered to build, push and deploy the service.
- **Secrets Management**: GitHub Secrets and environment variables are used to manage credentials and sensitive configurations.


## License

This project is private and proprietary. Unauthorised copying, modification, distribution or use of this software, via any medium, is strictly prohibited without explicit written permission from the owner.


## Contact

For any questions or clarifications about the project, please [reach out](https://www.mariuszilinskas.com/contact) to the project owner.


------
###### © 2024–present Marius Zilinskas. All rights reserved.