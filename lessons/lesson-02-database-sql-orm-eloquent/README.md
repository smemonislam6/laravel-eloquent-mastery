# Laravel 13 Eloquent Mastery

> 🚀 **Lesson 02 — Laravel Model Basics & Naming Conventions**

![Laravel](https://img.shields.io/badge/Laravel-13-red)
![Level](https://img.shields.io/badge/Level-Beginner-success)
![Language](https://img.shields.io/badge/Language-Bangla%20%2B%20English-blue)

---

# 🎯 Learning Objectives

এই Lesson শেষে আপনি জানতে পারবেন—

* ✅ What is a Model?
* ✅ Why Models are important?
* ✅ Laravel Naming Conventions
* ✅ How Models map to Database Tables
* ✅ Creating Models
* ✅ Model Properties
* ✅ Best Practices

---

# 📚 Table of Contents

1. What is a Model?
2. Why Use Models?
3. Laravel Naming Conventions
4. Creating a Model
5. How Laravel Finds the Table
6. Model Properties
7. Custom Table Name
8. Primary Key
9. Timestamps
10. Best Practices
11. Summary

---

# 📖 Chapter 1 — What is a Model?

Model হলো আপনার Application এবং Database-এর মধ্যে একটি Bridge।

আপনি Database-এর সাথে সরাসরি কাজ করেন না।

বরং Model-এর মাধ্যমে Database-এর Data Read, Insert, Update এবং Delete করেন।

> Think of a Model as a representation of a Database Table.

---

## Example

Database Table

```text
students
```

Laravel Model

```php
Student
```

একটি **Student Model** `students` table-এর প্রতিনিধিত্ব করে।

---

# 📖 Chapter 2 — Why Use Models?

Model ব্যবহার করলে—

* Database Query লিখতে সহজ হয়।
* Code অনেক বেশি Readable হয়।
* Business Logic এক জায়গায় রাখা যায়।
* Relationships সহজে তৈরি করা যায়।
* Reusable Code লেখা যায়।

উদাহরণ—

```php
Student::all();
```

এর পরিবর্তে Raw SQL লিখতে হতো—

```sql
SELECT * FROM students;
```

---

# 📖 Chapter 3 — Laravel Naming Conventions

Laravel Convention অনুসরণ করলে অতিরিক্ত Configuration প্রয়োজন হয় না।

| Model      | Table        |
| ---------- | ------------ |
| Student    | students     |
| Teacher    | teachers     |
| Guardian   | guardians    |
| Subject    | subjects     |
| ClassRoom  | class_rooms  |
| FeePayment | fee_payments |

### Rule

* Model → Singular (Student)
* Table → Plural (students)
* Model → PascalCase
* Table → snake_case

---

# 📖 Chapter 4 — Creating a Model

নতুন Model তৈরি করতে Artisan Command ব্যবহার করুন।

```bash
php artisan make:model Student
```

Migration সহ Model তৈরি করতে—

```bash
php artisan make:model Student -m
```

Controller সহ—

```bash
php artisan make:model Student -mc
```

সবকিছু একসাথে—

```bash
php artisan make:model Student -mcrfs
```

---

# 📖 Chapter 5 — How Laravel Finds the Table

ধরুন আপনার Model—

```php
class Student extends Model
{
}
```

Laravel Automatically ধরে নেয়—

```text
Model  : Student
Table  : students
```

আপনাকে আলাদা করে Table Name লিখতে হয় না।

---

# 📖 Chapter 6 — Model Properties

Laravel Model-এর কিছু গুরুত্বপূর্ণ Property—

## Table Name

```php
protected $table = 'students';
```

---

## Primary Key

```php
protected $primaryKey = 'id';
```

---

## Fillable

Mass Assignment Protection-এর জন্য।

```php
protected $fillable = [
    'name',
    'email',
    'phone',
];
```

---

## Hidden

API Response থেকে Field Hide করতে।

```php
protected $hidden = [
    'password',
];
```

---

## Casts

Data Type Conversion-এর জন্য।

```php
protected function casts(): array
{
    return [
        'email_verified_at' => 'datetime',
        'is_active' => 'boolean',
    ];
}
```

---

# 📖 Chapter 7 — Custom Table Name

যদি Table Name Convention Follow না করে—

Database Table

```text
tbl_students
```

তাহলে Model-এ লিখতে হবে—

```php
class Student extends Model
{
    protected $table = 'tbl_students';
}
```

---

# 📖 Chapter 8 — Custom Primary Key

যদি Primary Key `id` না হয়—

```php
protected $primaryKey = 'student_id';
```

Laravel তখন `student_id` ব্যবহার করবে।

---

# 📖 Chapter 9 — Timestamps

Laravel Default ধরে নেয় Table-এ দুটি Column আছে—

```text
created_at

updated_at
```

যদি না থাকে—

```php
public $timestamps = false;
```

---

# 📖 Chapter 10 — Best Practices

✅ Follow Laravel Naming Convention

✅ Keep Business Logic Inside Models

✅ Use Fillable Instead of Guarded

✅ Keep Models Small and Focused

✅ Avoid Writing Raw SQL Unless Necessary

✅ Use Eloquent Relationships

---

# 📝 Summary

আজ আমরা শিখলাম—

* Model কী?
* Model কেন ব্যবহার করা হয়?
* Naming Convention
* Artisan দিয়ে Model তৈরি
* Automatic Table Mapping
* Fillable
* Hidden
* Casts
* Primary Key
* Timestamps

---

# 💡 Practice

Create the following Models:

* Student
* Teacher
* Guardian
* Subject
* ClassRoom

তারপর Laravel কোন Table Name Automatically ব্যবহার করছে তা লক্ষ্য করুন।

---

# 🚀 Next Lesson

➡️ **Lesson 03 — Retrieving Data (all(), get(), find(), first(), firstOrFail(), findOrFail())**

---

## 📚 Navigation

⬅️ Previous: [Lesson 01 — Database → SQL → ORM → Eloquent](../lesson-01-database-sql-orm-eloquent/README.md)

➡️ Next: Lesson 03 — Retrieving Data
