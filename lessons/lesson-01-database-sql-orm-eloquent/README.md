# Laravel 13 Eloquent Mastery

> 🚀 **Lesson 01 — Database → SQL → ORM → Eloquent (Beginner)**

![Laravel](https://img.shields.io/badge/Laravel-13-red)
![Level](https://img.shields.io/badge/Level-Beginner-success)
![Language](https://img.shields.io/badge/Language-Bangla%20%2B%20English-blue)

---

# 🎯 Learning Objective

এই Lesson শেষে আপনি বুঝতে পারবেন—

* ✅ What is a Database?
* ✅ What is a DBMS?
* ✅ What is SQL?
* ✅ Why ORM exists?
* ✅ What is Laravel Eloquent?
* ✅ Raw SQL vs Query Builder vs Eloquent
* ✅ How Eloquent works internally

---

# 📚 Table of Contents

1. Database
2. DBMS
3. SQL
4. Problems with SQL
5. ORM
6. Eloquent
7. Raw SQL vs Query Builder vs Eloquent
8. Real World Example
9. Eloquent in MVC
10. Advantages of Eloquent

---

# 📖 Chapter 1 — What is a Database?

ধরুন আপনি একটি **School Management System** তৈরি করছেন।

আপনাকে নিচের তথ্যগুলো সংরক্ষণ করতে হবে—

* 👨‍🎓 Students
* 👨‍🏫 Teachers
* 👨‍👩‍👧 Guardians
* 📚 Subjects
* 🏫 Classes
* 📅 Attendance
* 📝 Exams
* 💳 Fees

প্রশ্ন হচ্ছে—

**এগুলো কোথায় সংরক্ষণ করবেন?**

উত্তর:

> ✅ **Database**

Database হলো এমন একটি জায়গা যেখানে তথ্য নিরাপদভাবে সংরক্ষণ করা হয়।

---

## Example

### students Table

| id | name  | email                                     |
| -- | ----- | ----------------------------------------- |
| 1  | Emon  | [emon@gmail.com](mailto:emon@gmail.com)   |
| 2  | Rahim | [rahim@gmail.com](mailto:rahim@gmail.com) |
| 3  | Karim | [karim@gmail.com](mailto:karim@gmail.com) |

এই Table-টি Database-এর একটি অংশ।

---

# 📖 Chapter 2 — What is DBMS?

Database নিজে নিজে কাজ করতে পারে না।

Database পরিচালনা করার জন্য একটি Software লাগে।

এটিকেই বলা হয়—

> **DBMS (Database Management System)**

Laravel-এ সবচেয়ে বেশি ব্যবহৃত DBMS—

* MySQL
* MariaDB
* PostgreSQL
* SQLite
* SQL Server

✅ এই সিরিজে আমরা **MySQL** ব্যবহার করব।

---

# 📖 Chapter 3 — What is SQL?

**SQL = Structured Query Language**

Database-এর সাথে কথা বলার ভাষা।

---

## Insert

```sql
INSERT INTO students (name,email)
VALUES ('Emon','emon@gmail.com');
```

---

## Select

```sql
SELECT * FROM students;
```

---

## Find by ID

```sql
SELECT * FROM students
WHERE id = 1;
```

---

## Update

```sql
UPDATE students
SET name='Ayaan'
WHERE id=1;
```

---

## Delete

```sql
DELETE FROM students
WHERE id=1;
```

এসবই SQL Query।

---

# 📖 Chapter 4 — Problems with SQL

ছোট Project-এ SQL লেখা সহজ।

কিন্তু Production Project-এ—

* Students
* Teachers
* Guardians
* Attendance
* Exams
* Fees
* Payments

মিলে ২০০+ Table থাকতে পারে।

তখন Query অনেক বড় হয়ে যায়।

## Example

```sql
SELECT *
FROM students
WHERE status='active'
AND class_id=3
ORDER BY name;
```

আরও বড় Query—

```sql
SELECT *
FROM students
LEFT JOIN guardians
ON guardians.id = students.guardian_id
LEFT JOIN attendances
ON attendances.student_id = students.id
WHERE students.status='active'
ORDER BY students.name;
```

❌ Query বড় হয়

❌ Maintain করা কঠিন

❌ Error হওয়ার সম্ভাবনা বাড়ে

---

# 📖 Chapter 5 — What is ORM?

**ORM = Object Relational Mapping**

ORM Database Table-কে PHP Object হিসেবে ব্যবহার করতে দেয়।

অর্থাৎ—

Table ➜ Object

Row ➜ Object

Column ➜ Property

Laravel-এর ORM-এর নাম—

> ✅ **Eloquent**

---

# 📖 Chapter 6 — What is Eloquent?

Eloquent হলো Laravel-এর Official ORM।

এটি SQL Query নিজে তৈরি করে।

---

## SQL

```sql
SELECT * FROM students;
```

### Eloquent

```php
Student::all();
```

---

## SQL

```sql
SELECT * FROM students
WHERE id=1;
```

### Eloquent

```php
Student::find(1);
```

---

## SQL

```sql
INSERT INTO students(name,email)
VALUES('Emon','emon@gmail.com');
```

### Eloquent

```php
Student::create([
    'name' => 'Emon',
    'email' => 'emon@gmail.com'
]);
```

---

## SQL

```sql
UPDATE students
SET name='Ayaan'
WHERE id=1;
```

### Eloquent

```php
Student::find(1)->update([
    'name' => 'Ayaan'
]);
```

---

## SQL

```sql
DELETE FROM students
WHERE id=1;
```

### Eloquent

```php
Student::find(1)->delete();
```

---

# 📖 Chapter 7 — Raw SQL vs Query Builder vs Eloquent

## Raw SQL

```php
DB::select("SELECT * FROM students");
```

✅ Powerful

❌ Hard to Maintain

---

## Query Builder

```php
DB::table('students')
    ->where('status','active')
    ->get();
```

✅ Flexible

✅ Fast

---

## Eloquent

```php
Student::where('status','active')->get();
```

✅ Readable

✅ Clean

✅ Relationships

✅ Production Friendly

---

# 📖 Chapter 8 — How Eloquent Works?

```text
Student::find(1)

        │

        ▼

Student Model

        │

        ▼

students Table

        │

        ▼

Generate SQL

SELECT * FROM students
WHERE id=1
LIMIT 1;

        │

        ▼

Database

        │

        ▼

Result

        │

        ▼

PHP Object

$student->name
$student->email
$student->phone
```

Laravel আপনার হয়ে SQL তৈরি করে।

আপনি শুধু Object নিয়ে কাজ করেন।

---

# 📖 Chapter 9 — Eloquent in MVC

```text
Browser
    │
    ▼
Route
    │
    ▼
Controller
    │
    ▼
Model (Eloquent)
    │
    ▼
Database
    │
    ▼
Model
    │
    ▼
Controller
    │
    ▼
View / API Response
```

## Example

```php
public function index()
{
    $students = Student::all();

    return response()->json($students);
}
```

Flow—

* Controller receives the request.
* Model uses Eloquent.
* Eloquent queries the Database.
* Database returns the data.
* Controller returns JSON or View.

---

# 📖 Chapter 10 — Advantages of Eloquent

✅ Less SQL Writing

✅ Easy to Read

✅ Easy to Maintain

✅ Supports Relationships

✅ Cleaner Code

✅ Production Ready

✅ Reusable

✅ Works seamlessly with other Laravel Features

---

# 📝 Summary

এই Lesson-এ আমরা শিখেছি—

* Database
* DBMS
* SQL
* SQL Problems
* ORM
* Laravel Eloquent
* Raw SQL vs Query Builder vs Eloquent
* MVC Flow
* Advantages of Eloquent

---

# 🚀 Next Lesson

➡️ **Lesson 02 — Laravel Model Basics & Naming Conventions**
