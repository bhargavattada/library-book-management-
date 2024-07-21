# Library Book Management System

This project, the "Library Book Management System," is a Python application designed to efficiently manage a library's collection of books. It provides a user-friendly interface for library staff to perform various operations related to book management. Below are the key features and functionalities of this system:

## Features

### 1. Add a New Book

Library staff can add new books to the library's collection. The following details can be provided for each book:
- Book Title
- Author
- Year of Publication
- ISBN (optional, but must be unique)

### 2. View All Books

Users can view a list of all the books available in the library. This list includes information about each book, such as its title, author, year of publication, and ISBN.

### 3. Search for a Book

Users can search for books based on specific criteria, including:
- Book Title
- Author
- Year of Publication
- ISBN

The system displays a list of matching books, making it easy to find specific titles.

### 4. Update Book Information

Library staff can update the information of a book, including its title, author, year of publication, and ISBN. This feature ensures that the library's records remain accurate and up-to-date.

### 5. Delete a Book

Books can be removed from the library's collection when needed. To delete a book, the staff can use the book's ISBN, ensuring a straightforward and efficient process.

### 6. Help (Issue)

This option provides information on how to use the system, particularly for deleting records using ISBN.

### 7. Exit

Users can gracefully exit the application at any time.

## How to Run

To run this Library Book Management System, follow these steps:

1. Ensure you have Python installed on your system.
2. Run the provided Python script.
3. Use the provided interface to perform various library book management tasks.


----------------------------------------------------------------------------------------------------------------


### Import Necessary Libraries
```python
from tkinter import *
import sqlite3
import tkinter.ttk as ttk
```

### Create or Connect to the Database
```python
def Database():
    global cursor, conn
    conn = sqlite3.connect(mydb)
    cursor = conn.cursor()
    cursor.execute("CREATE TABLE IF NOT EXISTS books (Book_name TEXT, Author TEXT, Year INT, ISBN INT PRIMARY KEY) ")
```

In the `Database` function, you establish a connection to an SQLite database and create a table called "books" if it doesn't already exist. This table will store information about books.

### Adding a New Book (Create)
```python
def add(): 
    # ...
    cursor.execute("INSERT INTO books (Book_name, Author, Year, ISBN) VALUES (?,?,?,?)",
                   (str(title_var.get()), str(author_var.get()), str(year_var.get()), str(isbn_var.get())))
    # ...
```

The `add` function inserts a new book into the database when the user clicks the "Add" button.

### Displaying All Books (Read)
```python
def display():
    book_rack.delete(*book_rack.get_children())
    Database()
    cursor.execute("SELECT * FROM books ORDER BY Book_name ASC")
    rows = cursor.fetchall()
    # ...
```

The `display` function retrieves all books from the database and displays them in the user interface.

### Deleting a Book (Delete)
```python
def delete():
    Database()
    cursor.execute("DELETE FROM books WHERE ISBN = ?", (isbn_var.get(),))
    # ...
```

The `delete` function removes a book from the database when the user clicks the "Delete" button.

### Searching for Books (Read)
```python
def SearchData():
    Database()
    cursor.execute("SELECT * FROM books WHERE Book_name = ? OR Author = ? OR Year = ? OR ISBN = ?",
                   (str(title_var.get()), str(author_var.get()), str(year_var.get()), str(isbn_var.get())))
    # ...
```

The `SearchData` function allows users to search for books based on criteria such as title, author, year, or ISBN.

These code snippets illustrate the fundamental CRUD (Create, Read, Update, Delete) operations for managing library books within your project. Users can add, view, search, and delete books from the library's collection.
