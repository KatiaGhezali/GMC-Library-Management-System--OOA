# Implementation Design

## 1. Introduction

This document presents the proposed implementation design of the Library Management System (LMS).

The system is modeled using Object-Oriented Programming (OOP) principles. JavaScript code examples are provided to demonstrate how the main classes and operations could be implemented.

The purpose of these examples is to illustrate the system's design and logic. A complete application, user interface, and database implementation are outside the scope of this project.

## 2. Object-Oriented Design

The system uses the following OOP principles:

### 2.1 Encapsulation

Encapsulation means keeping an object's internal data protected and providing methods to interact with it.

For example, a `BookCopy` object controls its availability through methods rather than allowing other objects to change its status arbitrarily.

### 2.2 Abstraction

Abstraction means exposing essential operations while hiding unnecessary implementation details.

For example, the `LoanService` provides `borrowBook()` and `returnBook()` methods without requiring users to know how database operations are performed.

### 2.3 Inheritance

Inheritance allows a class to reuse properties and methods from another class.

In a larger implementation, a common `User` class could contain shared properties such as an ID, name, and email. `Member` and `Librarian` could inherit from it.

For this simplified design, Member and Librarian are modeled as separate classes to keep their responsibilities clear.

### 2.4 Polymorphism

Polymorphism allows different objects to provide different implementations of the same method.

For example, if Member and Librarian inherit from a common User class, each could implement a different `getRole()` method.

## 3. Main Class Implementations

The following examples demonstrate the main classes of the system.

### 3.1 Book Class

The `Book` class represents a title in the library catalog.

```javascript
class Book {
  constructor(bookId, title, author, ISBN, category) {
    this.bookId = bookId;
    this.title = title;
    this.author = author;
    this.ISBN = ISBN;
    this.category = category;
  }

  getDetails() {
    return {
      bookId: this.bookId,
      title: this.title,
      author: this.author,
      ISBN: this.ISBN,
      category: this.category,
    };
  }

  updateDetails(title, author, category) {
    this.title = title;
    this.author = author;
    this.category = category;
  }
}
```

### 3.2 BookCopy Class

The `BookCopy` class represents an individual physical copy of a book.

```javascript
class BookCopy {
  constructor(copyId, book) {
    this.copyId = copyId;
    this.book = book;
    this.status = "AVAILABLE";
  }

  isAvailable() {
    return this.status === "AVAILABLE";
  }

  markAsIssued() {
    if (!this.isAvailable()) {
      throw new Error("Book copy is not available.");
    }

    this.status = "ISSUED";
  }

  markAsAvailable() {
    if (this.status !== "ISSUED") {
      throw new Error("Book copy is not currently issued.");
    }

    this.status = "AVAILABLE";
  }

  markAsMaintenance() {
    if (this.status === "RETIRED") {
      throw new Error("Retired copies cannot enter maintenance.");
    }

    this.status = "MAINTENANCE";
  }
}
```

### 3.3 Member Class

The `Member` class represents a registered library member.

```javascript
class Member {
  constructor(memberId, name, email, phone) {
    this.memberId = memberId;
    this.name = name;
    this.email = email;
    this.phone = phone;
    this.loans = [];
  }

  getLoanHistory() {
    return this.loans;
  }

  addLoan(loan) {
    this.loans.push(loan);
  }

  getActiveLoanCount() {
    return this.loans.filter((loan) => loan.status === "ACTIVE").length;
  }
}
```

### 3.4 Librarian Class

The `Librarian` class represents a staff member who manages library operations.

```javascript
class Librarian {
  constructor(librarianId, name, email) {
    this.librarianId = librarianId;
    this.name = name;
    this.email = email;
  }

  addBook(catalog, book) {
    catalog.addBook(book);
  }

  registerMember(member) {
    return member;
  }
}
```

### 3.5 Loan Class

The `Loan` class represents a borrowing transaction.

```javascript
class Loan {
  constructor(loanId, member, bookCopy, borrowDate, dueDate) {
    this.loanId = loanId;
    this.member = member;
    this.bookCopy = bookCopy;
    this.borrowDate = borrowDate;
    this.dueDate = dueDate;
    this.returnDate = null;
    this.status = "ACTIVE";
  }

  markAsReturned(returnDate = new Date()) {
    if (this.status !== "ACTIVE") {
      throw new Error("This loan is already closed.");
    }

    if (returnDate < this.borrowDate) {
      throw new Error("Return date cannot precede borrow date.");
    }

    this.returnDate = returnDate;
    this.status = "RETURNED";
  }

  calculateOverdueDays(currentDate = new Date()) {
    if (this.status !== "ACTIVE" || currentDate <= this.dueDate) {
      return 0;
    }

    const millisecondsPerDay = 1000 * 60 * 60 * 24;

    return Math.ceil((currentDate - this.dueDate) / millisecondsPerDay);
  }
}
```

### 3.6 Catalog Class

The `Catalog` class manages the collection of books.

```javascript
class Catalog {
  constructor() {
    this.books = [];
  }

  addBook(book) {
    this.books.push(book);
  }

  searchByTitle(title) {
    return this.books.filter((book) =>
      book.title.toLowerCase().includes(title.toLowerCase()),
    );
  }

  searchByAuthor(author) {
    return this.books.filter((book) =>
      book.author.toLowerCase().includes(author.toLowerCase()),
    );
  }
}
```

## 4. Loan Service

The `LoanService` coordinates borrowing and returning operations.

It validates requests and communicates with the relevant objects.

The following example uses in-memory objects to demonstrate the business logic.

```javascript
class LoanService {
  constructor(maxLoans = 3) {
    this.maxLoans = maxLoans;
    this.loans = [];
    this.nextLoanId = 1;
  }

  borrowBook(member, bookCopy, borrowDate = new Date()) {
    if (member.getActiveLoanCount() >= this.maxLoans) {
      throw new Error("Member has reached the borrowing limit.");
    }

    if (!bookCopy.isAvailable()) {
      throw new Error("Book copy is not available.");
    }

    const dueDate = new Date(borrowDate);
    dueDate.setDate(dueDate.getDate() + 14);

    const loan = new Loan(
      this.nextLoanId++,
      member,
      bookCopy,
      borrowDate,
      dueDate,
    );

    bookCopy.markAsIssued();
    member.addLoan(loan);
    this.loans.push(loan);

    return loan;
  }

  returnBook(loan, returnDate = new Date()) {
    if (loan.status !== "ACTIVE") {
      throw new Error("This loan is not active.");
    }

    if (returnDate < loan.borrowDate) {
      throw new Error("Return date cannot precede borrow date.");
    }

    loan.markAsReturned(returnDate);
    loan.bookCopy.markAsAvailable();

    return loan;
  }
}
```

## 5. Example Usage

The following example demonstrates how the classes work together.

```javascript
// Create a book
const book = new Book(
  1,
  "Clean Code",
  "Robert C. Martin",
  "9780132350884",
  "Software Engineering",
);

// Create a physical copy
const copy = new BookCopy(101, book);

// Register a member
const member = new Member(1, "John Smith", "john@example.com", "123456789");

// Create the loan service
const loanService = new LoanService(3);

// Borrow the book
const loan = loanService.borrowBook(member, copy);

console.log("Loan created:", loan.loanId);
console.log("Copy status:", copy.status);

// Return the book
loanService.returnBook(loan);

console.log("Loan status:", loan.status);
console.log("Copy status:", copy.status);
```

**Expected output (assuming the operations succeed):**

```text
Loan created: 1
Copy status: ISSUED
Loan status: RETURNED
Copy status: AVAILABLE
```

This example demonstrates how the objects collaborate to complete a borrowing and returning workflow.

## 6. Borrowing and Returning Pseudocode

### 6.1 Borrow Book

```text
FUNCTION borrowBook(member, bookCopy)

    IF member is not registered
        RETURN "Member not found"
    END IF

    IF member has reached borrowing limit
        RETURN "Borrowing limit reached"
    END IF

    IF bookCopy is not AVAILABLE
        RETURN "Book copy is unavailable"
    END IF

    CREATE a new Loan

    SET bookCopy status TO ISSUED

    SAVE the loan

    RETURN "Borrowing successful"

END FUNCTION
```

### 6.2 Return Book

```text
FUNCTION returnBook(loan)

    IF loan does not exist
        RETURN "Loan not found"
    END IF

    IF loan status is not ACTIVE
        RETURN "Loan already closed"
    END IF

    RECORD the return date

    SET loan status TO RETURNED

    IF book is in good condition
        SET bookCopy status TO AVAILABLE
    ELSE
        SET bookCopy status TO MAINTENANCE
    END IF

    SAVE the changes

    RETURN "Return successful"

END FUNCTION
```

## 7. Implementation Considerations

Although the code examples demonstrate the main object-oriented design, a real Library Management System would require additional functionality.

### 7.1 Database Integration

The current examples store information in memory.

A real implementation would use a database to persist information between application sessions.

Repositories would handle operations such as creating, retrieving, updating, and deleting records.

### 7.2 Authentication and Authorization

The system would require secure authentication and role-based authorization.

Members should only access their own loan information, while librarians should have permission to manage library records.

### 7.3 Data Validation

The system should validate user input, email addresses, ISBN values, and borrowing requests.

### 7.4 Error Handling

The application should handle invalid operations and unexpected errors without losing data or entering an inconsistent state.

### 7.5 Database Transactions

Borrowing and returning operations should use database transactions.

For example, creating a loan and changing a book copy's status should succeed or fail together.

This prevents a situation where a loan is created but the book copy remains incorrectly marked as available.

### 7.6 Concurrency

If two members attempt to borrow the same physical copy at the same time, the system must ensure that only one borrowing request succeeds.

Database transactions and appropriate locking or constraints can help prevent this problem.

## 8. Design Principles Applied

The proposed implementation follows these principles:

| Principle                       | Application                                                  |
| ------------------------------- | ------------------------------------------------------------ |
| Encapsulation                   | Objects manage their own data and state.                     |
| Single Responsibility Principle | Each class has a focused responsibility.                     |
| Separation of Concerns          | Business operations are handled separately from data access. |
| Reusability                     | Classes can be reused across different operations.           |
| Maintainability                 | The system is divided into manageable components.            |

## 9. Conclusion

The implementation design demonstrates how Object-Oriented Programming can be applied to the Library Management System.

The proposed classes represent the main entities, while the Loan Service coordinates the core borrowing and returning operations.

The JavaScript examples and pseudocode provide a foundation for a future implementation.

The project focuses on analysis, modeling, and architectural design rather than delivering a complete working application.
