# 📚 Library Management System

A Windows Forms desktop application built with C# and SQL Server for managing a library's books, members, and book issue/return operations.

👤 Developer

Name: Alisha Sajjad
Roll Number:[F23BDOCS1M01084]

🛠️ Technologies Used

Language: C# (.NET 10)
UI Framework: Windows Forms
Database: Microsoft SQL Server
Data Access: Microsoft.Data.SqlClient (ADO.NET)
Architecture: Two-project solution (App.Core + App.WindowsApp)

📋 Features

- 🔐 **Login System** — Secure librarian login with username and password
- 📊 **Dashboard** — Live counters showing total books, members, and issued books
- 📖 **Books Management** — Add, edit, delete, and search books with category and quantity tracking
- 👤 **Members Management** — Add, edit, delete, and view library members
- 🔄 **Issue & Return** — Issue books to members and mark them as returned
- 🗂️ **Categories** — Organize books by category

🗄️ Database Setup

1. Open **SQL Server Management Studio (SSMS)** or Visual Studio SQL query window
2. Run the following script:

```sql
CREATE DATABASE LibraryDB;
GO

USE LibraryDB;
GO

CREATE TABLE Categories (
    Id INT PRIMARY KEY IDENTITY(1,1),
    CategoryName NVARCHAR(100) NOT NULL
);

CREATE TABLE Books (
    Id INT PRIMARY KEY IDENTITY(1,1),
    BookTitle NVARCHAR(200) NOT NULL,
    AuthorName NVARCHAR(100) NOT NULL,
    Category NVARCHAR(100) NOT NULL,
    Quantity INT NOT NULL DEFAULT 0
);

CREATE TABLE Members (
    MemberID INT PRIMARY KEY IDENTITY(1,1),
    Name NVARCHAR(100) NOT NULL,
    Email NVARCHAR(100),
    Phone NVARCHAR(20),
    Address NVARCHAR(200),
    JoiningDate DATE DEFAULT GETDATE()
);

CREATE TABLE IssueReturn (
    IssueID INT PRIMARY KEY IDENTITY(1,1),
    BookId INT NOT NULL,
    MemberID INT NOT NULL,
    IssueDate DATE DEFAULT GETDATE(),
    ReturnDate DATE,
    IsReturned BIT DEFAULT 0,
    FOREIGN KEY (BookId) REFERENCES Books(Id),
    FOREIGN KEY (MemberID) REFERENCES Members(MemberID) ON DELETE CASCADE
);

CREATE TABLE Librarians (
    Id INT PRIMARY KEY IDENTITY(1,1),
    Username NVARCHAR(50) NOT NULL,
    Password NVARCHAR(50) NOT NULL
);

INSERT INTO Librarians (Username, Password) VALUES ('admin', '123');


## ▶️ How to Run

1. Clone the repository
2. Open `LibraryManagementSystem.slnx` in **Visual Studio 2022**
3. Run the database script above in SQL Server
4. Press **F5** to run
5. Login with:
   - **Username:** admin
   - **Password:** 123



## 📁 Project Structure


LibraryManagementSystem/
├── App.Core/                  # Business logic layer
│   ├── Interfaces/            # Service interfaces
│   ├── Models/                # Data models
│   └── Services/              # Service implementations
└── App.WindowsApp/            # UI layer
    └── Forms/
        ├── LoginForm.cs       # Login screen
        ├── Dashboard.cs       # Main dashboard
        ├── BooksForm.cs       # Books management
        ├── MembersForm.cs     # Members management
        └── IssueReturnForm.cs # Issue & return management
