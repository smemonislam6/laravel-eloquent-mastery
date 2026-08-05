# 🚀 Laravel Hack #06 — `paginate()` vs `simplePaginate()` vs `cursorPaginate()`

> Beginner Friendly | Laravel 13

---

# 🎯 Definition

Laravel-এ Large Dataset Display করার জন্য Pagination ব্যবহার করা হয়।

Laravel তিন ধরনের Pagination Support করে—

* ✅ `paginate()`
* ✅ `simplePaginate()`
* ✅ `cursorPaginate()`

সবগুলোর উদ্দেশ্য একই হলেও Performance এবং Use Case আলাদা।

---

# 📦 `paginate()`

Laravel-এর Default Pagination।

```php
$students = Student::paginate(10);
```

Generated SQL

```sql
SELECT *
FROM students
LIMIT 10 OFFSET 0;
```

Laravel অতিরিক্ত একটি Query চালায় Total Record Count বের করার জন্য।

```sql
SELECT COUNT(*) FROM students;
```

Features

* Total Records
* Current Page
* Last Page
* Previous / Next Links
* Page Numbers

---

# 📦 `simplePaginate()`

যখন Total Record Count দরকার নেই।

```php
$students = Student::simplePaginate(10);
```

Generated SQL

```sql
SELECT *
FROM students
LIMIT 10 OFFSET 0;
```

এখানে **COUNT(*) Query** চালানো হয় না।

Features

* Previous
* Next

❌ Total Page জানা যায় না।

---

# 📦 `cursorPaginate()`

Large Dataset-এর জন্য Laravel-এর সবচেয়ে Efficient Pagination।

```php
$students = Student::orderBy('id')
    ->cursorPaginate(10);
```

Generated SQL

প্রথম Page

```sql
SELECT *
FROM students
ORDER BY id ASC
LIMIT 10;
```

পরবর্তী Page

```sql
SELECT *
FROM students
WHERE id > 10
ORDER BY id ASC
LIMIT 10;
```

এটি OFFSET ব্যবহার করে না।

---

# 🔍 Difference

| Feature         | `paginate()` | `simplePaginate()` | `cursorPaginate()` |
| --------------- | ------------ | ------------------ | ------------------ |
| COUNT Query     | ✅ Yes        | ❌ No               | ❌ No               |
| OFFSET          | ✅ Yes        | ✅ Yes              | ❌ No               |
| Page Numbers    | ✅ Yes        | ❌ No               | ❌ No               |
| Previous / Next | ✅ Yes        | ✅ Yes              | ✅ Yes              |
| Performance     | ⭐⭐⭐⭐☆        | ⭐⭐⭐⭐⭐              | ⭐⭐⭐⭐⭐⭐             |
| Large Dataset   | ⚠️ Good      | ✅ Better           | 🚀 Best            |

---

# 💻 Example

## `paginate()`

```php
$students = Student::paginate(20);
```

Perfect For

* Admin Panel
* CMS
* Dashboard

---

## `simplePaginate()`

```php
$students = Student::simplePaginate(20);
```

Perfect For

* Blog List
* News Feed
* Product List

---

## `cursorPaginate()`

```php
$students = Student::orderBy('id')
    ->cursorPaginate(20);
```

Perfect For

* Social Feed
* Timeline
* Chat Messages
* Activity Logs
* Millions of Records

---

# 📊 How They Work

## `paginate()`

```text
Database
     │
COUNT(*)
     │
LIMIT + OFFSET
     │
Page Numbers
```

---

## `simplePaginate()`

```text
Database
     │
LIMIT + OFFSET
     │
Previous / Next
```

---

## `cursorPaginate()`

```text
Database
     │
WHERE id > Last Cursor
     │
LIMIT
     │
Next Cursor
```

---

# 🧠 Best Practice

## ✅ Use `paginate()`

যখন User-কে Total Page দেখাতে হবে।

Examples

* Student Management
* Employee Management
* Admin Dashboard
* Data Tables

---

## ✅ Use `simplePaginate()`

যখন শুধু Previous / Next Button যথেষ্ট।

Examples

* Blog
* Articles
* News
* Products

---

## ✅ Use `cursorPaginate()`

যখন Table-এ লক্ষ বা কোটি Record থাকতে পারে।

Examples

* Facebook Feed
* Twitter Timeline
* Notifications
* Chat Messages
* Audit Logs

---

# 📌 When to Use

| Situation          | Recommended        |
| ------------------ | ------------------ |
| Student List       | `paginate()`       |
| Admin Panel        | `paginate()`       |
| Blog Posts         | `simplePaginate()` |
| Product Listing    | `simplePaginate()` |
| Infinite Scroll    | `cursorPaginate()` |
| Activity Logs      | `cursorPaginate()` |
| Large API Response | `cursorPaginate()` |

---

# ⚠️ Common Mistakes

## ❌ Mistake 1

```php
Student::all()->paginate(20);
```

`paginate()` Collection-এর উপর কাজ করে না।

---

## ✅ Correct

```php
Student::paginate(20);
```

---

## ❌ Mistake 2

```php
Student::cursorPaginate(20);
```

`cursorPaginate()` ব্যবহার করার আগে Stable Ordering থাকা উচিত।

---

## ✅ Correct

```php
Student::orderBy('id')
    ->cursorPaginate(20);
```

---

## ❌ Mistake 3

Large Table-এ

```php
Student::paginate(100);
```

যখন Table-এ কয়েক মিলিয়ন Record থাকে, `COUNT(*)` Query Performance কমিয়ে দিতে পারে।

---

## ✅ Better

```php
Student::orderBy('id')
    ->cursorPaginate(100);
```

---

# 📈 Performance Comparison

| Feature          | `paginate()` | `simplePaginate()` | `cursorPaginate()` |
| ---------------- | ------------ | ------------------ | ------------------ |
| Speed            | ⭐⭐⭐⭐☆        | ⭐⭐⭐⭐⭐              | 🚀🚀🚀🚀🚀         |
| Memory           | Medium       | Low                | Lowest             |
| COUNT Query      | Yes          | No                 | No                 |
| Infinite Scroll  | ❌            | ❌                  | ✅                  |
| Production Ready | ✅            | ✅                  | ✅                  |

---

# 🚀 Performance Tips

✅ Admin Panel-এর জন্য `paginate()` ব্যবহার করুন।

✅ Blog বা Product Listing-এর জন্য `simplePaginate()` যথেষ্ট।

✅ Large Dataset বা Infinite Scroll-এর জন্য `cursorPaginate()` ব্যবহার করুন।

✅ `cursorPaginate()` ব্যবহার করার সময় সবসময় একটি Unique বা Indexed Column (`id`, `created_at`) দিয়ে `orderBy()` করুন।

```php
$students = Student::orderBy('id')
    ->cursorPaginate(20);
```

---

# 📝 Summary

* ✅ `paginate()` Total Count এবং Page Number দেখায়।
* ✅ `simplePaginate()` দ্রুত, কিন্তু Total Count দেয় না।
* ✅ `cursorPaginate()` Large Dataset-এর জন্য সবচেয়ে Efficient।
* ✅ Infinite Scroll-এর জন্য `cursorPaginate()` ব্যবহার করুন।
* ✅ Admin CRUD-এর জন্য `paginate()` এখনও সবচেয়ে জনপ্রিয়।

---

# 💡 Quick Remember

```text
paginate()

COUNT(*)
     │
LIMIT + OFFSET
     │
1 2 3 4 5
```

```text
simplePaginate()

LIMIT + OFFSET
     │
Previous / Next
```

```text
cursorPaginate()

WHERE id > Cursor
     │
LIMIT
     │
Next Cursor
```

---

# 🎯 Interview Question

### Question

কখন `cursorPaginate()` ব্যবহার করবেন?

### Answer

যখন আপনার Table-এ **Large Dataset (লক্ষ বা কোটি Record)** থাকে অথবা **Infinite Scroll API** তৈরি করছেন।

কারণ `cursorPaginate()` `OFFSET` এবং `COUNT(*)` Query এড়িয়ে Cursor-এর মাধ্যমে পরবর্তী Data Fetch করে, যা বড় Dataset-এ অনেক বেশি Efficient।

---

# 🔥 Pro Tip

> **Admin Panel → `paginate()`**
> **Blog / Product List → `simplePaginate()`**
> **Social Feed / API / Infinite Scroll → `cursorPaginate()`**
