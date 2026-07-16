# Cliente JDBC CRUD

A foundational Java exercise practicing raw JDBC data access: manual SQL, `PreparedStatement`, and `ResultSet` handling for a full CRUD flow, validated with integration tests against a real PostgreSQL database.

## Overview

The project implements a `ClienteDAO` behind an `IClienteDAO` interface, handling client registration, lookup, update, deletion, and listing directly through JDBC, with no ORM or abstraction layer in between. It was a step toward understanding what an ORM like JPA/Hibernate later automates.

## Features

- Full CRUD flow (`cadastrar`, `buscar`, `atualizar`, `excluir`, `buscarTodos`) implemented with hand-written SQL and `PreparedStatement`
- `ConnectionFactory` managing a single reusable JDBC connection, reopening it if closed
- Explicit resource cleanup (`ResultSet`, `PreparedStatement`, `Connection`) in `finally` blocks
- Integration tests with JUnit exercising the DAO against a real PostgreSQL database, covering create, read, update, delete, and list-all flows end to end

## Tech Stack

- Java 21
- JDBC
- PostgreSQL
- Maven
- JUnit 4

## Project Structure

```
backendProject3/
└── src/
    ├── main/java/br/com/.../
    │   ├── dao/generic/jdbc/
    │   │   ├── ConnectionFactory.java
    │   │   └── dao/
    │   │       ├── ClienteDAO.java
    │   │       └── IClienteDAO.java
    │   ├── domain/
    │   │   └── Cliente.java
    │   └── Main.java
    └── test/java/br/com/.../
        └── ClienteTest.java
```

## How to Run

1. Have PostgreSQL running locally and create a database matching the one configured in `ConnectionFactory`.
2. Set your own database credentials as environment variables or a local, git-ignored config file (never commit real credentials).
3. Run the tests with Maven:

```bash
mvn test
```

## Notes

This project was developed as part of my full stack Java formation, focused on practicing raw JDBC before moving on to generic DAO abstractions and later JPA/Hibernate.

## Important: Before Publishing

- **Remove the hardcoded database credentials** from `ConnectionFactory.java` and rotate the exposed password, before making this repository public
- Externalize the JDBC URL, username, and password to environment variables or a `.gitignore`-excluded properties file
- Clean up the leftover IntelliJ boilerplate comments in `Main.java`
