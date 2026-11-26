# Requirements Analysis

## 1. Introduction

The Library Management System (LMS) is designed to simplify the management of library resources, members, and borrowing activities.

It provides librarians with tools to maintain the book catalog, register members, and manage loans. Members can search the catalog, check book availability, borrow books, and return them.

## 2. System Actors

### 2.1 Librarian

The librarian is responsible for managing the library's operations.

Responsibilities:

- Add new books to the catalog.
- Update book information.
- Remove books from the catalog when appropriate.
- Register new members.
- Update member information.
- View borrowing transactions.
- Issue books to members.
- Process returned books.
- Identify overdue loans.

### 2.2 Member

A member is a registered library user.

Responsibilities:

- Search for books.
- View book details.
- Check book availability.
- Borrow available books.
- Return borrowed books.
- View personal borrowing history.

## 3. Functional Requirements

Functional requirements describe what the system must do.

| ID    | Requirement            | Description                                                 |
| ----- | ---------------------- | ----------------------------------------------------------- |
| FR-01 | Manage Books           | The librarian can add, update, and remove books.            |
| FR-02 | Manage Members         | The librarian can register, update, and deactivate members. |
| FR-03 | Search Books           | Members can search by title, author, or ISBN.               |
| FR-04 | Check Availability     | The system displays whether a book is available.            |
| FR-05 | Borrow Book            | A member can borrow an available book.                      |
| FR-06 | Return Book            | A member can return a borrowed book.                        |
| FR-07 | Manage Loans           | The system records borrowing and return dates.              |
| FR-08 | Track Overdue Loans    | The system identifies loans past their due date.            |
| FR-09 | View Borrowing History | Members can view their previous loans.                      |
| FR-10 | View Active Loans      | Librarians can view current borrowing transactions.         |

## 4. Non-Functional Requirements

Non-functional requirements describe how the system should operate.

- **Usability:** The interface should be easy to understand.
- **Security:** Only authorized librarians can access administrative functions.
- **Reliability:** Borrowing and returning operations must preserve accurate records.
- **Performance:** Book searches should return results efficiently.
- **Maintainability:** The system should be organized into independent components.
- **Data Integrity:** A physical book copy must not be loaned to two members simultaneously.
- **Scalability:** The architecture should allow additional features in the future.

## 5. Business Rules

The system must follow these rules:

1. Only registered and active members can borrow books.
2. Only available book copies can be borrowed.
3. A book copy can have only one active loan at a time.
4. Every loan must have a borrowing date and due date.
5. Returning a book must update its availability.
6. A loan is overdue when its due date has passed and it has not been returned.
7. Only librarians can add, update, or remove catalog records.
8. A member cannot borrow a book if their borrowing privileges are suspended.

For this simplified design, the maximum number of active loans and the loan period are configurable library policies rather than hard-coded values.

## 6. Main Use Cases

| Use Case          | Actor             | Description                             |
| ----------------- | ----------------- | --------------------------------------- |
| Search Book       | Member            | Search the catalog.                     |
| View Book Details | Member            | View book information and availability. |
| Borrow Book       | Member, Librarian | Complete a borrowing transaction.       |
| Return Book       | Member, Librarian | Complete a return transaction.          |
| Add Book          | Librarian         | Add a book to the catalog.              |
| Update Book       | Librarian         | Modify book information.                |
| Remove Book       | Librarian         | Remove a book from the catalog.         |
| Register Member   | Librarian         | Create a member account.                |
| View Loans        | Librarian         | Review active and previous loans.       |
| View History      | Member            | Review personal borrowing history.      |

## 7. Assumptions and Constraints

- Each member has a unique member ID.
- Each book has a unique ISBN.
- A book may have multiple physical copies.
- Each physical copy has a unique copy ID.
- The system maintains borrowing records.
- A member must be registered before borrowing.
- The project models a single library branch.
- Online payments, reservations, and inter-library loans are outside the initial scope.

## 8. Conclusion

The requirements analysis identifies the main actors, system responsibilities, and business rules. These requirements provide the foundation for the architecture and UML models.
