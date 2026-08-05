# 🚀 Laravel Hack #04 — `first()` vs `find()`

> Beginner Friendly | Laravel 13

---

# 🎯 Definition

`first()` এবং `find()`—দুটোই একটি **Single Model Object** Return করে।

কিন্তু তাদের কাজ এক নয়।

অনেক Beginner `find()` এবং `first()` একই মনে করেন।

❌ বাস্তবে এদের Use Case সম্পূর্ণ আলাদা।

---

# 📦 `find()`

`find()` শুধুমাত্র **Primary Key** ব্যবহার করে Record খুঁজে বের করে।

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

# 📦 `first()`

`first()` Query-এর **প্রথম Matching Record** Return করে।

```php
$student = Student::where('status', 'active')
    ->first();
```

Generated SQL

```sql
SELECT *
FROM students
WHERE status = 'active'
LIMIT 1;
```

যদি কোনো Record না থাকে—

```php
null
```

Return করবে।

---

# 🔍 Difference

| `find()`                                 | `first()`                                 |
| ---------------------------------------- | ----------------------------------------- |
| Primary Key দিয়ে Search করে             | Query-এর প্রথম Matching Record Return করে |
| `id` (বা Custom Primary Key) ব্যবহার করে | যেকোনো Condition ব্যবহার করা যায়         |
| `find($id)`                              | `where(...)->first()`                     |
| Query Builder ছাড়াও ব্যবহার করা যায়    | Query Builder-এর সাথে ব্যবহার করা হয়     |
| Primary Key Lookup-এর জন্য Best          | Filtered Query-এর জন্য Best               |

---

# 💻 Example

## `find()`

```php
$student = Student::find(5);
```

Generated SQL

```sql
SELECT *
FROM students
WHERE id = 5
LIMIT 1;
```

---

## `first()`

```php
$student = Student::where('class_id', 10)
    ->where('status', 'active')
    ->first();
```

Generated SQL

```sql
SELECT *
FROM students
WHERE class_id = 10
AND status = 'active'
LIMIT 1;
```

---

# 📌 Return Type

দুটোই Return করে—

```php
App\Models\Student|null
```

অর্থাৎ—

* Record থাকলে → `Student`
* Record না থাকলে → `null`

---

# 🧠 Best Practice

## ✅ `find()`

যখন আপনার কাছে Primary Key আছে।

```php
$student = Student::find($id);
```

Examples

* Student Details
* Teacher Profile
* Guardian Profile

---

## ✅ `first()`

যখন Condition অনুযায়ী প্রথম Record দরকার।

```php
$student = Student::where('email', $email)
    ->first();
```

Examples

* Login
* Search
* Reports
* Filtered Record

---

# 📌 When to Use

| Situation                 | Recommended         |
| ------------------------- | ------------------- |
| Find Student by ID        | `find()`            |
| Find Teacher by ID        | `find()`            |
| Find Active Student       | `first()`           |
| Find Student by Email     | `first()`           |
| Find Latest Active Record | `latest()->first()` |

---

# ⚠️ Common Mistakes

## ❌ Mistake 1

```php
Student::find($email);
```

`find()` শুধু Primary Key দিয়ে কাজ করে।

---

## ✅ Correct

```php
Student::where('email', $email)
    ->first();
```

---

## ❌ Mistake 2

```php
Student::where('id', 1)
    ->first();
```

এটি কাজ করবে, কিন্তু আরও সংক্ষিপ্ত উপায় আছে।

---

## ✅ Better

```php
Student::find(1);
```

---

# 📈 Performance Comparison

| Feature               | `find()`    | `first()`  |
| --------------------- | ----------- | ---------- |
| Lookup by Primary Key | ✅ Excellent | ✅ Possible |
| Flexible Query        | ❌           | ✅          |
| Readability           | ⭐⭐⭐⭐⭐       | ⭐⭐⭐⭐☆      |
| Performance           | ⭐⭐⭐⭐⭐       | ⭐⭐⭐⭐☆      |
| Production Ready      | ✅           | ✅          |

---

# 📝 Summary

* ✅ `find()` শুধুমাত্র Primary Key দিয়ে Search করে।
* ✅ `first()` প্রথম Matching Record Return করে।
* ✅ দুটোই `Model Object` Return করে।
* ✅ Primary Key থাকলে `find()` ব্যবহার করুন।
* ✅ Custom Condition থাকলে `first()` ব্যবহার করুন।

---

# 💡 Quick Remember

```text
find()

Primary Key
     │
     ▼
SELECT * FROM students
WHERE id = ?
LIMIT 1;
```

```text
first()

where(...)
orderBy(...)
latest()
     │
     ▼
First Matching Record
```

---

# 🎯 Interview Question

### Question

নিচের কোনটি বেশি উপযুক্ত?

```php
Student::find(10);
```

নাকি

```php
Student::where('id', 10)->first();
```

### Answer

যদি Primary Key দিয়ে Record খুঁজতে হয়, তাহলে **`find()` ব্যবহার করুন**।

কারণ এটি আরও পরিষ্কার (Readable), উদ্দেশ্য স্পষ্ট (Intent-Revealing), এবং Primary Key Lookup-এর জন্য Laravel-এর Recommended Method।
