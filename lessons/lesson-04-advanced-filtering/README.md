# Laravel 13 Eloquent Mastery

> 🚀 **Lesson 03 — Retrieving Data with Eloquent**

![Laravel](https://img.shields.io/badge/Laravel-13-red)
![Level](https://img.shields.io/badge/Level-Beginner-success)
![Language](https://img.shields.io/badge/Language-Bangla%20%2B%20English-blue)

---

# 🎯 Learning Objectives

এই Lesson শেষে আপনি জানতে পারবেন—

* ✅ Retrieve all records
* ✅ Retrieve multiple records
* ✅ Retrieve a single record
* ✅ Handle missing records
* ✅ Get a single column value
* ✅ Get multiple values
* ✅ Check if data exists
* ✅ Best practices for production

---# Laravel 13 Eloquent Mastery

> 🚀 **Lesson 04 — Advanced Filtering with Eloquent**

![Laravel](https://img.shields.io/badge/Laravel-13-red)
![Level](https://img.shields.io/badge/Level-Intermediate-orange)
![Language](https://img.shields.io/badge/Language-Bangla%20%2B%20English-blue)

---

# 🎯 Learning Objectives

এই Lesson শেষে আপনি জানতে পারবেন—

* ✅ Filter records using `where()`
* ✅ Combine conditions with `orWhere()`
* ✅ Use `whereIn()` & `whereNotIn()`
* ✅ Filter ranges using `whereBetween()`
* ✅ Handle `NULL` values
* ✅ Filter by Date, Month & Year
* ✅ Conditional Queries with `when()`
* ✅ Relationship Filtering using `whereHas()`
* ✅ Production Best Practices

---

# 📚 Table of Contents

1. where()
2. orWhere()
3. whereIn()
4. whereNotIn()
5. whereBetween()
6. whereNull()
7. whereNotNull()
8. whereDate()
9. whereMonth()
10. whereYear()
11. when()
12. unless()
13. whereHas()
14. has()
15. whereColumn()
16. Best Practices

---

# 📖 Chapter 1 — `where()`

সবচেয়ে বেশি ব্যবহৃত Filtering Method।

```php
$students = Student::where('status', 'active')->get();
```

Generated SQL

```sql
SELECT * FROM students
WHERE status = 'active';
```

---

# 📖 Chapter 2 — `orWhere()`

একাধিক Condition-এর মধ্যে OR ব্যবহার করতে।

```php
$students = Student::where('status', 'active')
    ->orWhere('status', 'pending')
    ->get();
```

---

# 📖 Chapter 3 — `whereIn()`

একাধিক Value দিয়ে Filter করতে।

```php
$students = Student::whereIn('class_id', [1, 2, 3])->get();
```

---

# 📖 Chapter 4 — `whereNotIn()`

```php
$students = Student::whereNotIn('class_id', [4, 5])->get();
```

---

# 📖 Chapter 5 — `whereBetween()`

Range অনুযায়ী Filter করতে।

```php
$students = Student::whereBetween('age', [10, 15])->get();
```

Date Range

```php
$students = Student::whereBetween('created_at', [
    '2026-01-01',
    '2026-12-31'
])->get();
```

---

# 📖 Chapter 6 — `whereNull()`

```php
$students = Student::whereNull('deleted_at')->get();
```

---

# 📖 Chapter 7 — `whereNotNull()`

```php
$students = Student::whereNotNull('phone')->get();
```

---

# 📖 Chapter 8 — `whereDate()`

```php
$students = Student::whereDate('created_at', today())->get();
```

---

# 📖 Chapter 9 — `whereMonth()`

```php
$students = Student::whereMonth('created_at', 8)->get();
```

---

# 📖 Chapter 10 — `whereYear()`

```php
$students = Student::whereYear('created_at', 2026)->get();
```

---

# 📖 Chapter 11 — `when()`

Condition সত্য হলে Query Apply করবে।

```php
$students = Student::query()
    ->when(request('class_id'), function ($query, $classId) {
        $query->where('class_id', $classId);
    })
    ->get();
```

✅ Dynamic Search-এর জন্য খুবই উপযোগী।

---

# 📖 Chapter 12 — `unless()`

Condition মিথ্যা হলে Query Apply করবে।

```php
$students = Student::query()
    ->unless(auth()->user()->isAdmin(), function ($query) {
        $query->where('status', 'active');
    })
    ->get();
```

---

# 📖 Chapter 13 — `whereHas()`

Relationship-এর উপর ভিত্তি করে Filter করতে।

```php
$students = Student::whereHas('guardian', function ($query) {
    $query->where('occupation', 'Teacher');
})->get();
```

---

# 📖 Chapter 14 — `has()`

যেসব Student-এর Guardian আছে।

```php
$students = Student::has('guardian')->get();
```

---

# 📖 Chapter 15 — `whereColumn()`

দুটি Column Compare করতে।

```php
$students = Student::whereColumn(
    'created_at',
    'updated_at'
)->get();
```

---

# 📖 Chapter 16 — Best Practices

| Method           | Best Use Case          |
| ---------------- | ---------------------- |
| `where()`        | Basic Filtering        |
| `orWhere()`      | Alternative Conditions |
| `whereIn()`      | Multiple Values        |
| `whereBetween()` | Range Filtering        |
| `whereNull()`    | NULL Check             |
| `whereDate()`    | Date Filtering         |
| `when()`         | Dynamic Queries        |
| `whereHas()`     | Relationship Filtering |

---

# 💡 Performance Tips

* ✅ Database Index ব্যবহার করুন Frequently Filtered Columns-এ।
* ✅ `select()` দিয়ে প্রয়োজনীয় Column-ই আনুন।
* ✅ N+1 Query এড়াতে `with()` ব্যবহার করুন।
* ✅ `when()` ব্যবহার করে Clean Dynamic Query লিখুন।

---

# 📝 Summary

আজ আমরা শিখলাম—

* Basic & Advanced Filtering
* Dynamic Queries
* Date Filtering
* Relationship Filtering
* Production Best Practices

---

# 🚀 Next Lesson

➡️ **Lesson 05 — Ordering, Limiting & Pagination**

---

## 📚 Navigation

⬅️ Previous: [Lesson 03 — Retrieving Data](../lesson-03-retrieving-data/README.md)

➡️ Next: Lesson 05 — Ordering, Limiting & Pagination


# 📚 Table of Contents

1. Retrieving Data
2. `all()`
3. `get()`
4. `find()`
5. `findOrFail()`
6. `first()`
7. `firstOrFail()`
8. `value()`
9. `pluck()`
10. `exists()`
11. `doesntExist()`
12. Best Practices
13. Summary

---

# 📖 Chapter 1 — Retrieving Data

Laravel Eloquent-এর সবচেয়ে সাধারণ কাজ হলো Database থেকে Data আনা (Retrieve Data)।

Eloquent বিভিন্ন পরিস্থিতির জন্য আলাদা Method প্রদান করে।

---

# 📖 Chapter 2 — `all()`

Table-এর **সব Record** নিয়ে আসে।

```php
$students = Student::all();
```

Generated SQL

```sql
SELECT * FROM students;
```

✅ ছোট Table-এর জন্য ভালো।

❌ বড় Table-এ ব্যবহার করা উচিত নয়।

---

# 📖 Chapter 3 — `get()`

Condition সহ Multiple Record আনতে ব্যবহৃত হয়।

```php
$students = Student::where('status', 'active')->get();
```

Generated SQL

```sql
SELECT *
FROM students
WHERE status='active';
```

✅ Production-এ `get()` অনেক বেশি ব্যবহৃত হয়।

---

# 📖 Chapter 4 — `find()`

Primary Key দিয়ে একটি Record নিয়ে আসে।

```php
$student = Student::find(1);
```

Generated SQL

```sql
SELECT *
FROM students
WHERE id = 1
LIMIT 1;
```

যদি Record না পাওয়া যায়—

```php
null
```

Return করবে।

---

# 📖 Chapter 5 — `findOrFail()`

Primary Key দিয়ে Record খুঁজে।

```php
$student = Student::findOrFail(1);
```

যদি Record না থাকে—

Laravel Automatically

```text
404 Not Found
```

Exception Throw করবে।

✅ API এবং Resource Controller-এর জন্য Recommended।

---

# 📖 Chapter 6 — `first()`

প্রথম Record নিয়ে আসে।

```php
$student = Student::first();
```

Generated SQL

```sql
SELECT *
FROM students
LIMIT 1;
```

Condition সহ—

```php
$student = Student::where('status', 'active')
    ->first();
```

যদি Record না থাকে—

```php
null
```

Return করবে।

---

# 📖 Chapter 7 — `firstOrFail()`

```php
$student = Student::where('status', 'active')
    ->firstOrFail();
```

Record না থাকলে—

```text
404 Not Found
```

Throw করবে।

---

# 📖 Chapter 8 — `value()`

একটি মাত্র Column-এর Value নিয়ে আসে।

```php
$email = Student::where('id', 1)
    ->value('email');
```

Generated SQL

```sql
SELECT email
FROM students
WHERE id=1
LIMIT 1;
```

✅ শুধু একটি Value দরকার হলে `value()` ব্যবহার করুন।

---

# 📖 Chapter 9 — `pluck()`

একটি Column-এর সব Value Collection আকারে নিয়ে আসে।

```php
$names = Student::pluck('name');
```

বা

```php
$students = Student::pluck('name', 'id');
```

Generated SQL

```sql
SELECT id, name
FROM students;
```

Use Cases

* Dropdown List
* Select Options
* Reports

---

# 📖 Chapter 10 — `exists()`

Data আছে কি না Check করতে।

```php
$isExists = Student::where('email', 'emon@gmail.com')
    ->exists();
```

Return

```php
true
```

অথবা

```php
false
```

✅ Count করার চেয়ে `exists()` বেশি Efficient।

---

# 📖 Chapter 11 — `doesntExist()`

Data না থাকলে—

```php
$isMissing = Student::where('email', 'test@gmail.com')
    ->doesntExist();
```

Return

```php
true
```

অথবা

```php
false
```

---

# 📖 Chapter 12 — Best Practices

| Method          | Use Case                   |
| --------------- | -------------------------- |
| `all()`         | Small Tables Only          |
| `get()`         | Multiple Records           |
| `find()`        | Find by Primary Key        |
| `findOrFail()`  | API / Resource Controllers |
| `first()`       | First Matching Record      |
| `firstOrFail()` | Required Record            |
| `value()`       | Single Column              |
| `pluck()`       | Dropdown / Collection      |
| `exists()`      | Existence Check            |
| `doesntExist()` | Missing Data Check         |

---

# 💡 Performance Tips

✅ Prefer `get()` instead of `all()` on large tables.

✅ Use `value()` when you only need one column.

✅ Use `exists()` instead of `count()` for existence checks.

✅ Prefer `findOrFail()` and `firstOrFail()` in Controllers to automatically return a 404 response when a record is not found.

---

# 📝 Summary

আজ আমরা শিখলাম—

* Retrieve All Records
* Retrieve Multiple Records
* Retrieve Single Record
* Handle Missing Records
* Get One Column
* Get Multiple Values
* Check Record Existence
* Production Best Practices

---

# 🚀 Next Lesson

➡️ **Lesson 04 — Advanced Filtering (`where()`, `orWhere()`, `whereIn()`, `whereBetween()`, `whereNull()`, `whereDate()` and more)**

---

## 📚 Navigation

⬅️ Previous: [Lesson 02 — Laravel Model Basics & Naming Conventions](../lesson-02-model-basics/README.md)

➡️ Next: Lesson 04 — Advanced Filtering
