# Library Management System - Diagrams

## 1. Overview

This directory is dedicated to the diagrams created during the analysis and architectural modeling of the Library Management System (LMS).

The diagrams illustrate the system's architecture, structure, functionality, data relationships, and behavior.

Most diagrams are embedded directly in the Markdown documentation files rather than stored as separate image files.

## 2. Diagram Categories

The project includes the following diagrams:

### Architecture Diagrams

- System Architecture Diagram
- Component Diagram
- Layered Architecture Diagram

Location: `docs/architecture.md`

### UML Diagrams

- Class Diagram
- Use Case Diagram
- Sequence Diagram: Borrow a Book
- Sequence Diagram: Return a Book
- State Diagram: Book Copy Lifecycle

Location: `docs/uml-diagrams.md`

### Data and Functional Diagrams

- Entity-Relationship Diagram (ERD)
- Functional Decomposition Diagram
- BookCopy Lifecycle Diagram
- Loan Lifecycle Diagram

Location: `docs/data-model.md`

## 3. Diagram Technologies

The project uses the following diagram technologies:

- **Mermaid:** Used for architecture, class, sequence, state, entity-relationship, and functional diagrams.
- **PlantUML:** Used for the use case diagram.

These tools allow diagrams to be maintained as text, making them easier to edit and version-control with Git.

## 4. How to View the Diagrams

### GitHub

GitHub supports Mermaid diagrams directly inside Markdown files.

To view them:

1. Open the repository on GitHub.
2. Navigate to the `docs/` directory.
3. Open the relevant Markdown file.
4. Scroll to the diagram sections.

### PlantUML

The use case diagram uses PlantUML syntax.

To render it:

1. Copy the PlantUML code from `docs/uml-diagrams.md`.
2. Open the [PlantUML Online Server](https://www.plantuml.com/plantuml/uml/).
3. Paste the code into the editor.
4. View the generated diagram.

## 5. Purpose

The diagrams provide a visual representation of the proposed system before implementation.

They help identify:

- System components and their relationships.
- Main classes and their responsibilities.
- Interactions between actors and the system.
- Workflows for borrowing and returning books.
- Data entities and their relationships.
- Object states and transitions.

Together, these diagrams support the analysis and architectural design of the Library Management System.
