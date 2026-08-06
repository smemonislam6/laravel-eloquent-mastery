# 💻 Laravel Eloquent Mastery — Practice Questions & Interview Challenges

> **Topics Covered**
>
> * Database → SQL → ORM → Eloquent
> * Model Basics
> * Retrieving Data
> * Advanced Filtering
> * Ordering, Limiting & Pagination
> * Model vs Eloquent
> * Model Object vs Collection
> * all() vs get()
> * first() vs find()
> * latest() vs orderBy()
> * paginate() vs simplePaginate() vs cursorPaginate()
> * value() vs pluck()
> * exists() vs count()

---

# 💻 Practice Questions

## 🏫 Question 01 — School Management System

আপনি একটি **Student List API** তৈরি করছেন।

### Requirements

* শুধুমাত্র Active Student দেখাতে হবে।
* Name অনুযায়ী A-Z Sort হবে।
* প্রতি Page-এ ২০টি Student দেখাতে হবে।

> **Think:** কোন Eloquent Methods ব্যবহার করবেন?

---

## 🛒 Question 02 — POS System

একটি POS Software-এ Cashier Product Search করছে।

### Requirements

* শুধুমাত্র Available Product দেখাতে হবে।
* Product Name অনুযায়ী Sort হবে।
* প্রথম ১০টি Product দেখাতে হবে।

---

## 🏥 Question 03 — Hospital Management

Doctor Dashboard-এ আজকে Admit হওয়া সর্বশেষ ১৫ জন Patient দেখাতে হবে।

---

## 🍽 Question 04 — Restaurant Management

Kitchen Dashboard-এ Pending Order আছে কিনা Check করতে হবে।

Order Count দরকার নেই।

---

## 👨‍💼 Question 05 — HR Management

Employee Registration করার আগে Email Exists কিনা Verify করতে হবে।

---

## 🛍 Question 06 — Ecommerce

Homepage-এ সর্বশেষ Publish হওয়া ১২টি Product দেখাতে হবে।

---

## 🏫 Question 07 — School Management

Class 10-এর সকল Student Roll Number অনুযায়ী দেখাতে হবে।

---

## 🏥 Question 08 — Hospital

Patient ID দিয়ে Patient Profile Retrieve করতে হবে।

---

## 🍽 Question 09 — Restaurant

Dashboard-এ আজকের মোট Completed Order দেখাতে হবে।

---

## 🛒 Question 10 — POS

Product Category Dropdown তৈরি করতে হবে।

Dropdown-এ ID এবং Category Name থাকবে।

---

# 🔥 Real Life Challenges

## 🚀 Challenge 01 — Student Search API

### Requirements

* Name Search
* Active Student Only
* Latest Admission First
* ১০টি Result প্রতি Page

---

## 🚀 Challenge 02 — Ecommerce Product Listing

### Requirements

* Active Products
* Category Filter
* Brand Filter
* Price ASC
* Pagination

---

## 🚀 Challenge 03 — Employee Directory

### Requirements

* Employee Search
* Department Filter
* Designation Filter
* Latest Joining First

---

## 🚀 Challenge 04 — Restaurant Dashboard

Dashboard-এ দেখাতে হবে—

* Total Orders
* Pending Order Exists?
* Completed Orders
* Latest ৫টি Orders

---

## 🚀 Challenge 05 — Hospital Patient List

### Requirements

* Latest Admit
* Doctor Filter
* Department Filter
* Pagination

---

## 🚀 Challenge 06 — School Result Module

### Requirements

* Active Student
* Class Filter
* Roll Number Sort
* Search
* Pagination

---

# 🎯 Interview Questions

## 🎤 Interview Question 01

আপনার কাছে **২০ লক্ষ Student Record** আছে।

User শুধু জানতে চায়—

> এই Student Database-এ আছে কি না।

**কোন Method ব্যবহার করবেন? কেন?**

---

## 🎤 Interview Question 02

Student ID ব্যবহার করে শুধু Email Retrieve করতে হবে।

**কোন Method সবচেয়ে Efficient?**

---

## 🎤 Interview Question 03

Country Dropdown তৈরি করতে হবে।

**কোন Method ব্যবহার করবেন?**

---

## 🎤 Interview Question 04

নিচের Route-এর জন্য কোন Method ব্যবহার করবেন?

```text
GET /students/15
```

---

## 🎤 Interview Question 05

Blog Homepage-এ সর্বশেষ Publish হওয়া Post দেখাতে হবে।

**কোন Method ব্যবহার করবেন?**

---

## 🎤 Interview Question 06

Admin Panel-এ Student List-এর সাথে Total Page Number দেখাতে হবে।

**কোন Pagination Method ব্যবহার করবেন?**

---

## 🎤 Interview Question 07

Facebook-এর মতো Infinite Scroll তৈরি করতে হবে।

**কোন Pagination Method ব্যবহার করবেন?**

---

## 🎤 Interview Question 08

৩০ লক্ষ Record-এর Table-এ শুধু Check করতে হবে—

> Record Exists?

**কোন Method ব্যবহার করবেন?**

---

## 🎤 Interview Question 09

নিচের Query Production-এ Problem কেন হতে পারে?

```php
Student::all()->where('status', 'active');
```

---

## 🎤 Interview Question 10

কোনটি বেশি Readable?

```php
Post::latest()->get();
```

অথবা

```php
Post::orderBy('created_at', 'desc')->get();
```

কোন পরিস্থিতিতে কোনটি ব্যবহার করবেন?

---

# 🚀 Bonus Coding Challenges

## 🏫 Challenge 01 — Student Management API

Build a Student Module.

### Features

* Student List
* Student Details
* Active Student
* Latest Student
* Search
* Pagination
* Email Exists Check
* Student Count
* Student Dropdown

---

## 🛒 Challenge 02 — Ecommerce Product API

### Features

* Product Search
* Category Filter
* Latest Product
* Price Sorting
* Pagination
* Product Exists Check

---

## 🏥 Challenge 03 — Hospital Patient Module

### Features

* Patient Registration Check
* Patient Details
* Latest Admit
* Department Filter
* Pagination

---

## 🍽 Challenge 04 — Restaurant Order Module

### Features

* Pending Order Exists
* Latest Orders
* Today's Completed Orders
* Customer Dropdown
* Infinite Scroll API

---

## 👨‍💼 Challenge 05 — HR Employee Directory

### Features

* Employee Search
* Department Filter
* Latest Joining
* Employee Exists
* Employee Count
* Pagination

---

# 🏆 Final Interview Challenge

## 🎯 School Management System

Build a **Student Management REST API**.

### Requirements

* Student List API
* Student Details API
* Search by Name
* Search by Email
* Active/Inactive Filter
* Class Filter
* Latest Admission
* Roll Number Sorting
* Pagination
* Student Exists Check
* Total Student Count
* Student Dropdown (`id => name`)
* Latest 10 Students API

# 💡 Goal

এই Question Set Solve করতে পারলে আপনি—

* ✅ Laravel Eloquent Fundamentals ভালোভাবে বুঝবেন
* ✅ Real Project Scenario Handle করতে পারবেন
* ✅ Junior/Mid-Level Laravel Interview-এর জন্য প্রস্তুত হবেন
* ✅ Production-ready Query Writing Skill অর্জন করবেন
