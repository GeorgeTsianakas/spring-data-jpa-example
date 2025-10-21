# Spring Data JPA Example

Simple, production‑ready Spring Boot project that demonstrates clean usage of Spring Data JPA with layered architecture (domain → repository → service), plus alternative in‑memory map implementations for comparison.

![](https://img.shields.io/badge/Editor-IntelliJ-informational?style=flat&logo=intellij-idea)
![](https://img.shields.io/badge/Code-Java_8-informational?style=flat&logo=java)
![](https://img.shields.io/badge/Framework-Spring_Boot_2.2.6-informational?style=flat&logo=spring)
![](https://img.shields.io/badge/Persistence-JPA_|_Hibernate-informational)
![](https://img.shields.io/badge/Database-H2_(in--memory)-informational?logo=h2)
![](https://img.shields.io/badge/Build-Maven-informational?logo=apache-maven)

---

## Overview
This project is a concise example of how to structure a Spring Boot application using:
- Spring Data JPA repositories
- Service layer abstractions (CRUD service, JPA-backed services, and in‑memory map implementations)
- A simple domain model (Customer, Product, Order, User/Role)

It is ideal for learning and for serving as a starting template for small CRUD applications.

## Tech stack
- Java 8
- Spring Boot 2.2.6
- Spring Data JPA (Hibernate)
- H2 (in‑memory, runtime scope)
- Spring Security (basic setup, can be extended)
- Maven

## Project structure (high level)
- src/main/java/com/example/demo
  - config – common bean configuration
  - domain – entities and enums (Customer, Product, Order, etc.)
  - repositories – Spring Data JPA repositories
  - services
    - jpaservices – services backed by JPA repositories
    - mapservices – in‑memory map services for quick testing
    - reposervices – services backed directly by repositories (example pattern)
    - security – encryption service (Jasypt)
  - DemoApplication – Spring Boot entry point
- src/main/resources
  - application.properties – sets active profile to `springdatajpa`
- src/test – sample test scaffolding

## Profiles
By default the application runs with the `springdatajpa` profile (see application.properties). Other service implementations (mapservices, reposervices) are provided to illustrate alternative approaches and can be wired via profile or configuration if desired.

## Getting started
Prerequisites:
- JDK 8+
- Maven 3.6+ (or use the provided Maven Wrapper)

Build:
- Windows: `mvnw.cmd clean install`
- macOS/Linux: `./mvnw clean install`

Run (from project root):
- Windows: `mvnw.cmd spring-boot:run`
- macOS/Linux: `./mvnw spring-boot:run`

Alternatively, run the generated jar after build:
- Windows: `java -jar target/demo-0.0.1-SNAPSHOT.jar`
- macOS/Linux: `java -jar target/demo-0.0.1-SNAPSHOT.jar`

The app starts on port 8080 by default.

## Database
- Uses an in‑memory H2 database at runtime (no external setup required).
- Spring Boot auto-configures the datasource for H2 based on classpath.
- If you want to use the H2 web console, add the following to `src/main/resources/application.properties` and restart:
  - `spring.h2.console.enabled=true`
  - `spring.h2.console.path=/h2-console`

## Domain model (selected)
- Customer, Address
- Product, Cart, CartDetail
- Order, OrderDetail, OrderStatus (enum)
- User, Role

## Repositories and Services
- Repositories: `CustomerRepository`, `OrderRepository`, `ProductRepository`, `RoleRepsoitory`, `UserRepository`
- Services expose CRUD operations and multiple implementations:
  - `*JpaDaoImpl` – JPA‑backed services (active via `springdatajpa` profile)
  - `*MapImpl` – simple in‑memory map services (useful for demos/tests)
  - `*RepoImpl` – example services backed directly by repositories

## Configuration and Security
- Basic security dependencies are included; `EncryptionService` uses Jasypt. Extend as needed for your use case.
- Common bean configuration is centralized in `config/CommonBeanConfig.java`.

## Testing
Run unit tests:
- Windows: `mvnw.cmd test`
- macOS/Linux: `./mvnw test`

## Common Maven commands
- Clean and build: `mvnw.cmd clean install` (Windows) | `./mvnw clean install` (macOS/Linux)
- Run app: `mvnw.cmd spring-boot:run` | `./mvnw spring-boot:run`
- Run tests: `mvnw.cmd test` | `./mvnw test`

## Notes
- This repository is intended as an educational example; no explicit license file is included. Add a license before using it in production contexts.
- IntelliJ IDEA is recommended (project includes Maven Wrapper for easy setup).
