# Laravel 13 Eloquent Mastery

> 🚀 **Lesson 05 — Ordering, Limiting & Pagination**

---

# 🎯 Learning Objectives

এই Lesson শেষে আপনি জানতে পারবেন—

* ✅ Sort records using `orderBy()`
* ✅ Sort in descending order using `latest()` and `oldest()`
* ✅ Random ordering with `inRandomOrder()`
* ✅ Limit records using `limit()` and `take()`
* ✅ Skip records using `skip()` and `offset()`
* ✅ Paginate large datasets
* ✅ Difference between `paginate()`, `simplePaginate()` and `cursorPaginate()`
* ✅ Production Best Practices

---

# 📚 Table of Contents

1. orderBy()
2. latest()
3. oldest()
4. reorder()
5. inRandomOrder()
6. limit()
7. take()
8. skip()
9. offset()
10. paginate()
11. simplePaginate()
12. cursorPaginate()
13. Best Practices

---

# 📖 Chapter 1 — `orderBy()`

Ascending Order

```php
$students = Student::orderBy('name')->get();
```

Descending Order

```php
$students = Student::orderBy('name', 'desc')->get();
```

Generated SQL

```sql
SELECT *
FROM students
ORDER BY name ASC;
```

---

# 📖 Chapter 2 — `latest()`

Latest Record আনতে।

```php
$students = Student::latest()->get();
```

Default

```php
latest('created_at')
```

Custom Column

```php
$students = Student::latest('admission_date')->get();
```

---

# 📖 Chapter 3 — `oldest()`

সবচেয়ে পুরনো Record।

```php
$students = Student::oldest()->get();
```

---

# 📖 Chapter 4 — `reorder()`

আগের Ordering Remove করে নতুন Ordering Apply করতে।

```php
$students = Student::orderBy('name')
    ->reorder('created_at', 'desc')
    ->get();
```

---

# 📖 Chapter 5 — `inRandomOrder()`

Random Record আনতে।

```php
$students = Student::inRandomOrder()->get();
```

Use Cases

* Quiz Questions
* Random Products
* Featured Students

---

# 📖 Chapter 6 — `limit()`

নির্দিষ্ট সংখ্যক Record আনতে।

```php
$students = Student::limit(10)->get();
```

Generated SQL

```sql
SELECT *
FROM students
LIMIT 10;
```

---

# 📖 Chapter 7 — `take()`

`take()` হলো `limit()`-এর Alias।

```php
$students = Student::take(5)->get();
```

---

# 📖 Chapter 8 — `skip()`

শুরুর কিছু Record বাদ দিতে।

```php
$students = Student::skip(10)
    ->take(10)
    ->get();
```

---

# 📖 Chapter 9 — `offset()`

`offset()` ও `skip()` একই কাজ করে।

```php
$students = Student::offset(20)
    ->limit(10)
    ->get();
```

---

# 📖 Chapter 10 — `paginate()`

Laravel-এর Default Pagination।

```php
$students = Student::paginate(15);
```

Features

* Total Records
* Current Page
* Last Page
* Previous & Next Links

Production-এ Admin Panel-এর জন্য সবচেয়ে বেশি ব্যবহৃত হয়।

---

# 📖 Chapter 11 — `simplePaginate()`

যখন Total Count দরকার নেই।

```php
$students = Student::simplePaginate(15);
```

এটি `paginate()`-এর তুলনায় Faster।

---

# 📖 Chapter 12 — `cursorPaginate()`

Large Dataset-এর জন্য Recommended।

```php
$students = Student::orderBy('id')
    ->cursorPaginate(20);
```

Advantages

* Faster Performance
* Better Memory Usage
* Ideal for Large Tables

---

# 📖 Chapter 13 — Best Practices

| Method             | Best Use Case     |
| ------------------ | ----------------- |
| `orderBy()`        | Custom Sorting    |
| `latest()`         | Latest Records    |
| `oldest()`         | Oldest Records    |
| `inRandomOrder()`  | Random Data       |
| `limit()`          | Small Result Set  |
| `paginate()`       | Admin Panels      |
| `simplePaginate()` | Faster Pagination |
| `cursorPaginate()` | Large Datasets    |

---

# 💡 Performance Tips

* ✅ `latest()` ব্যবহার করলে `created_at` Index থাকলে Performance ভালো হয়।
* ✅ Large Table-এর জন্য `cursorPaginate()` ব্যবহার করুন।
* ✅ Pagination-এর আগে Filtering করুন।
* ✅ `select()` ব্যবহার করে শুধুমাত্র প্রয়োজনীয় Column আনুন।
* ✅ `inRandomOrder()` বড় Table-এ ব্যয়বহুল হতে পারে, প্রয়োজন হলে সতর্কতার সাথে ব্যবহার করুন।

---

# 📝 Summary

আজ আমরা শিখলাম—

* Sorting Records
* Limiting Records
* Random Ordering
* Pagination Methods
* Production Best Practices

---

# 🚀 Next Lesson

➡️ **Lesson 06 — Eloquent Relationships (One to One, One to Many & Many to Many)**

---

## 📚 Navigation

⬅️ Previous: [Lesson 04 — Advanced Filtering](../lesson-04-advanced-filtering/README.md)

➡️ Next: Lesson 06 — Eloquent Relationships
