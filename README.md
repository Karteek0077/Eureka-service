# Eureka Server

Service discovery server for the ecommerce microservices architecture.

## Port
- **8761**

## Description
Eureka Server is the service registry where all microservices register themselves. It enables service discovery and load balancing across the microservices ecosystem.

## Running the Service

```bash
mvn spring-boot:run
```

## Access
- Eureka Dashboard: http://localhost:8761

## Configuration
See `src/main/resources/application.properties` for configuration options.
