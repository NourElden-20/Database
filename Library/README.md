# 📚 Library Database Project

## 📌 Overview
This project is a simple **Library Management Database** built using **SQL Server** or **MySQL**.  
It contains 3 main tables:

- **Books** → stores information about each book.  
- **Members** → stores information about library members.  
- **Borrow** → stores borrowing transactions between members and books.  

The goal of this project is to practice **Database Design** and **SQL Queries**.

---

## 🛠️ How to Use
1. Clone this repository.  
2. Open `library.sql` in **SSMS** (SQL Server) or **phpMyAdmin** (MySQL / XAMPP).  
3. Run the `CREATE DATABASE` and `CREATE TABLE` statements.  
4. Insert the provided sample data into the tables.  
5. Solve the exercises listed below by writing SQL queries.  

---

## 📝 Database Schema
**Tables:**
- **books** (`book_id`, `title`, `author`, `price`)  
- **members** (`member_id`, `name`, `phone`)  
- **borrow** (`borrow_id`, `book_id`, `member_id`, `borrowDate`, `returnDate`)  

**Relationships:**
- One **member** can borrow many **books**.  
- One **book** can be borrowed many times.  

---

## 🎯 Exercises

### 🔹 Part 1: Basic Queries
1. Display all books from the `books` table. 
--SELECT * FROM books;
2. Display only the names of members from the `members` table.  
--SELECT NAME FROM members;
3. Display all columns from the `borrow` table.
SELECT book_id,borrow_id,borrowDate,member_id,returnDate from borrow;
4. Display books with a price greater than 100.  
SELECT * FROM books WHERE price >100;
5. Display members whose phone numbers start with "010".
--select * from members where phone like '010%'
-------------  

### 🔹 Part 2: Queries with JOIN
6. Display the book titles borrowed by members (book title + member name).
  --SELECT title , name FROM books JOIN borrow ON books.book_id=borrow.book_id JOIN members on borrow.member_id = members.member_id
7. Display all borrow records with the member name and borrow date only.
  --SELECT borrowDate , name FROM members JOIN borrow ON members.member_id=borrow.member_id 
8. Display the members who still have borrowed books (`returnDate` = null).
  --SELECT members.name 
FROM borrow 
JOIN members ON borrow.member_id = members.member_id
WHERE borrow.returnDate IS NULL;

9. Display each book and how many times it has been borrowed (book title + borrow count). 
SELECT books.title, COUNT(borrow.borrow_id) AS borrow_count
-- FROM books
-- LEFT JOIN borrow ON books.book_id = borrow.book_id
-- GROUP BY books.title;
10. Display members who have borrowed more than one book.  
 SELECT members.name, COUNT(borrow.borrow_id) AS total_borrows
-- FROM members
-- JOIN borrow ON members.member_id = borrow.member_id
-- GROUP BY members.name
-- HAVING COUNT(borrow.borrow_id) > 1;
### 🔹 Part 3: Data Modification
11. Update the price of the book with `book_id = 3` to 200.  
-- update books set price =200 where book_id = 3
12. Update the phone number of the member with `member_id = 2` to "01099998888". 
--update members set phone ='01099998888' where member_id = 2
13. Delete the book with `book_id = 5` (consider borrow dependencies). 
--delete from  books where book_id = 5 

### 🔹 Part 4: Advanced Queries
14. Display the member who borrowed the largest number of books.

SELECT members.name, COUNT(borrow.borrow_id) AS total_borrows
-- FROM members
-- JOIN borrow ON members.member_id = borrow.member_id
-- GROUP BY members.name
-- ORDER BY total_borrows DESC
-- LIMIT 1;

select name,COUNT(borrow.member_id) from members join borrow on members.member_id=borrow.borrow_id  
15. Display the latest borrow transaction (the most recent `borrowDate`).  
SELECT MAX(borrow.borrowDate)  FROM borrow 
16. Display all books that have never been borrowed.  
SELECT *  FROM books where book_id not in (select book_id from borrowe )
---

## 🚀 Future Improvements
- Add more tables (e.g., Librarians, Book Categories).  
- Add stored procedures and triggers.  
- Connect the database with a front-end application.  

---

## 🧑‍💻 Nour
This project is created for **SQL practice** and uploaded to GitHub for learning purposes.  
