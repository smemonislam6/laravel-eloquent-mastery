# 🚀 Laravel Hack #03 — `all()` vs `get()`

> Beginner Friendly | Laravel 13 

---

# 🎯 Definition

Laravel Eloquent-এ `all()` এবং `get()`—দুটোই Database থেকে Multiple Records নিয়ে আসে।

অনেক Beginner মনে করেন দুটো একই জিনিস।

❌ বাস্তবে তা নয়।

---

## 📦 `all()`

`all()` Table-এর **সব Record** Retrieve করে।

```php
$students = Student::all();
```

Generated SQL

```sql
SELECT * FROM students;
```

---

## 📦 `get()`

`get()` Query Execute করে এবং Query Builder-এর মাধ্যমে Filter করা Record Return করে।

```php
$students = Student::where('status', 'active')->get();
```

Generated SQL

```sql
SELECT *
FROM students
WHERE status = 'active';
```

---

# 🔍 Difference

| `all()`                       | `get()`                               |
| ----------------------------- | ------------------------------------- |
| সব Record Return করে          | Filtered অথবা Custom Query Return করে |
| কোনো Condition Support করে না | Condition Support করে                 |
| Query Builder ব্যবহার করে না  | Query Builder ব্যবহার করে             |
| Small Tables-এর জন্য উপযোগী   | Production-এর জন্য Recommended        |
| Less Flexible                 | Highly Flexible                       |

---

# 💻 Example

## `all()`

```php
$students = Student::all();
```

Return

```text
All Students
```

---

## `get()`

```php
$students = Student::where('status', 'active')
    ->orderBy('name')
    ->get();
```

Return

```text
Only Active Students
```

---

# 📌 Can You Chain Methods?

## ❌ `all()`

```php
Student::all()->where('status', 'active');
```

এটি Database-এ Filter করে না।

প্রথমে **সব Data Memory-তে Load** হবে, তারপর Collection Filter করবে।

---

## ✅ `get()`

```php
Student::where('status', 'active')
    ->get();
```

এখানে Filtering Database Level-এ হয়।

---

# 📊 Memory Usage

## `all()`

```php
Student::all();
```

Database

⬇

সব Record Load

⬇

PHP Memory

---

## `get()`

```php
Student::where('status', 'active')->get();
```

Database

⬇

শুধু দরকারি Record

⬇

PHP Memory

---

# 🧠 Best Practice

## ✅ Use `all()`

যখন—

* Table খুব ছোট
* Lookup Data
* Static Data
* Settings
* Countries
* Blood Groups

Example

```php
$countries = Country::all();
```

---

## ✅ Use `get()`

যখন—

* Search
* Reports
* Dashboard
* Student List
* Teacher List
* Attendance
* Fees
* Production Applications

Example

```php
$students = Student::where('class_id', 5)
    ->where('status', 'active')
    ->get();
```

---

# 📌 When to Use

| Situation       | Recommended |
| --------------- | ----------- |
| Countries Table | `all()`     |
| Roles Table     | `all()`     |
| Student List    | `get()`     |
| Search Feature  | `get()`     |
| Reports         | `get()`     |
| Dashboard       | `get()`     |

---

# ⚠️ Common Mistakes

## ❌ Mistake 1

```php
Student::all()
    ->where('status', 'active');
```

সব Record আগে Load হবে।

Performance খারাপ হবে।

---

## ✅ Correct

```php
Student::where('status', 'active')
    ->get();
```

---

## ❌ Mistake 2

```php
Student::all()
    ->take(10);
```

Database থেকে সব Record আসবে।

তারপর Collection প্রথম ১০টি নিবে।

---

## ✅ Correct

```php
Student::limit(10)
    ->get();
```

---

# 📈 Performance Comparison

| Feature          | `all()`   | `get()` |
| ---------------- | --------- | ------- |
| Performance      | ⭐⭐☆☆☆     | ⭐⭐⭐⭐⭐   |
| Memory Usage     | High      | Low     |
| Flexible         | ❌         | ✅       |
| Filtering        | ❌         | ✅       |
| Ordering         | ❌         | ✅       |
| Production Ready | ❌ Limited | ✅ Yes   |

---

# 📝 Summary

* ✅ `all()` সব Record নিয়ে আসে।
* ✅ `get()` Query Execute করে।
* ✅ `get()` Filtering Support করে।
* ✅ Large Dataset-এর জন্য `get()` ব্যবহার করুন।
* ✅ Production Application-এ `get()` বেশি ব্যবহৃত হয়।

---

# 💡 Quick Remember

```text
all()

Database
     │
     ▼
All Records
     │
     ▼
Collection
```

```text
where()
orderBy()
limit()
get()

Database
     │
     ▼
Filtered Records
     │
     ▼
Collection
```
