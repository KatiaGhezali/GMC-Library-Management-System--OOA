# GMC Library Management System (LMS)

## Overview

The Library Management System (LMS) is a conceptual software design project that models the management of a library's books, members, and borrowing transactions.

The purpose of this project is to apply Object-Oriented Analysis (OOA), UML modeling, and architectural design principles before moving toward implementation.

The system is designed to help librarians manage library resources efficiently while allowing members to search for books and borrow or return them.

## Project Objectives

- Identify the system's actors and functional requirements.
- Define the main use cases and system interactions.
- Design a layered software architecture.
- Identify classes, attributes, methods, and relationships.
- Create UML diagrams to represent system structure and behavior.
- Model the system's data and business processes.
- Demonstrate how the design could be translated into code.

## Main Actors

- **Librarian:** Manages books, members, and borrowing transactions.
- **Member:** Searches for books, borrows books, and returns books.

## Main Features

- Book catalog management.
- Member registration and management.
- Book searching and availability checking.
- Book borrowing and returning.
- Loan and due-date tracking.
- Overdue loan identification.

## System Architecture

The proposed system follows a layered architecture consisting of four layers:

1. **Presentation Layer:** Handles user interaction.
2. **Business Logic Layer:** Manages application operations and business rules.
3. **Data Access Layer:** Handles communication with the database.
4. **Database Layer:** Stores persistent system information.

## UML and Design Models

The project includes the following diagrams and models:

### Architecture Diagrams

- System Architecture Diagram.
- Component Diagram.
- Layered Architecture Diagram.

### UML Diagrams

- Use Case Diagram.
- Class Diagram.
- Sequence Diagram: Borrow a Book.
- Sequence Diagram: Return a Book.
- BookCopy State Diagram.

### Data, Functional, and Behavioral Models

- Entity-Relationship Diagram (ERD).
- Functional Decomposition Diagram.
- BookCopy Lifecycle Model.
- Loan Lifecycle Model.

## Repository Structure

```text
library-management-system/
├── README.md
├── docs/
│   ├── requirements.md
│   ├── architecture.md
│   ├── uml-diagrams.md
│   ├── data-model.md
│   └── implementation.md
└── diagrams/
    └── README.md
```

## Design Principles

The design follows these software engineering principles:

- **Encapsulation:** Objects manage their own data and expose controlled operations.
- **Single Responsibility Principle (SRP):** Each class has a clear responsibility.
- **Abstraction:** Complex implementation details are hidden behind simpler interfaces.
- **Separation of Concerns:** Presentation, business logic, and data access are separated.

## Project Scope

This checkpoint focuses on Object-Oriented Analysis, architectural planning, and system modeling.

It does not require a fully functional application, frontend interface, or deployed database. JavaScript examples and pseudocode are included to demonstrate how the proposed design could be implemented.

## Documentation

- [Requirements Analysis](docs/requirements.md)
- [System Architecture](docs/architecture.md)
- [UML Diagrams](docs/uml-diagrams.md)
- [Data, Functional, and Behavioral Models](docs/data-model.md)
- [Implementation Design](docs/implementation.md)
- [Diagram Documentation](diagrams/README.md)

## Technologies and Modeling Tools

- **JavaScript:** Used for illustrative implementation examples.
- **Mermaid:** Used to create architecture, class, sequence, state, and data diagrams.
- **PlantUML:** Used to create the use case diagram.
- **Markdown:** Used for project documentation and diagrams.

## Project Status

**Status:** Documentation and architectural modeling completed as a design checkpoint.

The project establishes a conceptual foundation for a future Library Management System implementation.
