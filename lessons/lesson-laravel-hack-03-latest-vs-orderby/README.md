# 🚀 Laravel Hack #05 — `latest()` vs `orderBy()`

> Beginner Friendly | Laravel 13

---

# 🎯 Definition

`latest()` এবং `orderBy()`—দুটোই Database Record Sort করার জন্য ব্যবহৃত হয়।

অনেক Developer `latest()` এবং `orderBy('created_at', 'desc')`-কে একই মনে করেন।

আংশিকভাবে এটি সত্য, কিন্তু তাদের উদ্দেশ্য (Purpose) এবং Use Case ভিন্ন।

---

# 📦 `latest()`

`latest()` হলো একটি Shortcut Method।

Defaultভাবে এটি `created_at` Column অনুযায়ী Descending Order-এ Data Sort করে।

```php
$students = Student::latest()->get();
```

Generated SQL

```sql
SELECT *
FROM students
ORDER BY created_at DESC;
```

---

Custom Column দিয়েও ব্যবহার করা যায়।

```php
$students = Student::latest('admission_date')->get();
```

Generated SQL

```sql
SELECT *
FROM students
ORDER BY admission_date DESC;
```

---

# 📦 `orderBy()`

`orderBy()` দিয়ে যেকোনো Column এবং যেকোনো Direction অনুযায়ী Sorting করা যায়।

Ascending Order

```php
$students = Student::orderBy('name')->get();
```

Generated SQL

```sql
SELECT *
FROM students
ORDER BY name ASC;
```

---

Descending Order

```php
$students = Student::orderBy('name', 'desc')->get();
```

Generated SQL

```sql
SELECT *
FROM students
ORDER BY name DESC;
```

---

Multiple Columns

```php
$students = Student::orderBy('class_id')
    ->orderBy('roll_no')
    ->get();
```

Generated SQL

```sql
SELECT *
FROM students
ORDER BY class_id ASC,
         roll_no ASC;
```

---

# 🔍 Difference

| `latest()`                    | `orderBy()`             |
| ----------------------------- | ----------------------- |
| Shortcut Method               | General Sorting Method  |
| Default Column = `created_at` | Any Column              |
| Default Order = DESC          | ASC or DESC             |
| Less Flexible                 | Highly Flexible         |
| Best for Latest Records       | Best for Custom Sorting |

---

# 💻 Example

## `latest()`

Show Latest Students

```php
$students = Student::latest()->get();
```

---

Show Latest Admissions

```php
$students = Student::latest('admission_date')->get();
```

---

## `orderBy()`

Sort by Name

```php
$students = Student::orderBy('name')->get();
```

---

Sort by Roll Number

```php
$students = Student::orderBy('roll_no')->get();
```

---

Sort by Class then Roll

```php
$students = Student::orderBy('class_id')
    ->orderBy('roll_no')
    ->get();
```

---

# 📌 Return Type

দুটোই Return করে—

```php
Illuminate\Database\Eloquent\Collection
```

---

# 🧠 Best Practice

## ✅ Use `latest()`

যখন—

* Recent Posts
* Latest Students
* Latest Orders
* Latest Payments
* Latest Admissions

Example

```php
$orders = Order::latest()->paginate(20);
```

---

## ✅ Use `orderBy()`

যখন—

* Name Sorting
* Roll Sorting
* Marks Sorting
* Price Sorting
* Custom Reports

Example

```php
$students = Student::orderBy('name')
    ->orderBy('roll_no')
    ->get();
```

---

# 📌 When to Use

| Situation               | Recommended |
| ----------------------- | ----------- |
| Latest Students         | `latest()`  |
| Latest Blog Posts       | `latest()`  |
| Sort by Name            | `orderBy()` |
| Sort by Roll            | `orderBy()` |
| Sort by Marks           | `orderBy()` |
| Multiple Column Sorting | `orderBy()` |

---

# ⚠️ Common Mistakes

## ❌ Mistake 1

Database Table-এ `created_at` Column নেই।

```php
Student::latest()->get();
```

এটি SQL Error দিতে পারে, কারণ Defaultভাবে `created_at` ব্যবহার করা হয়।

---

## ✅ Correct

```php
Student::latest('admission_date')->get();
```

---

## ❌ Mistake 2

```php
Student::latest('name')->get();
```

`latest()` Date/Time Column-এর জন্য বেশি অর্থবহ।

Alphabetical Sorting-এর জন্য এটি ব্যবহার করা উচিত নয়।

---

## ✅ Correct

```php
Student::orderBy('name')->get();
```

---

# 📈 Performance Comparison

| Feature          | `latest()`         | `orderBy()` |
| ---------------- | ------------------ | ----------- |
| Default Sorting  | `created_at DESC`  | Custom      |
| Any Column       | ✅ (Specify Column) | ✅           |
| Multiple Columns | ❌                  | ✅           |
| Readability      | ⭐⭐⭐⭐⭐              | ⭐⭐⭐⭐☆       |
| Flexibility      | ⭐⭐⭐☆☆              | ⭐⭐⭐⭐⭐       |
| Production Ready | ✅                  | ✅           |

---

# 🚀 Performance Tips

✅ `created_at` বা যেই Column দিয়ে Sort করবেন, সেখানে Database Index থাকলে Performance ভালো হবে।

✅ বড় Dataset-এর ক্ষেত্রে Sorting-এর পর `paginate()` বা `cursorPaginate()` ব্যবহার করুন।

```php
$students = Student::latest()->paginate(20);
```

---

# 📝 Summary

* ✅ `latest()` হলো `ORDER BY created_at DESC`-এর Shortcut।
* ✅ `orderBy()` যেকোনো Column Sort করতে পারে।
* ✅ Recent Data দেখাতে `latest()` ব্যবহার করুন।
* ✅ Custom Sorting-এর জন্য `orderBy()` ব্যবহার করুন।
* ✅ Multiple Column Sorting-এর জন্য `orderBy()`-ই সঠিক পছন্দ।

---

# 💡 Quick Remember

```text
latest()

created_at DESC
        │
        ▼
Newest Records
```

```text
orderBy()

Any Column
ASC / DESC
        │
        ▼
Custom Sorting
```

---

# 🎯 Interview Question

### Question

নিচের দুইটির মধ্যে কোনটি বেশি Readable?

```php
Post::orderBy('created_at', 'desc')->get();
```

নাকি

```php
Post::latest()->get();
```

### Answer

যদি `created_at DESC` অনুযায়ী Sort করতে চান, তাহলে **`latest()`** ব্যবহার করুন। এটি ছোট, পরিষ্কার এবং Laravel Convention অনুসরণ করে।

আর যদি অন্য কোনো Column বা Multiple Column অনুযায়ী Sort করতে চান, তাহলে **`orderBy()`** ব্যবহার করুন।
