# 🚀 Laravel Hack #07 — `value()` vs `pluck()`

> Beginner Friendly | Laravel 13 
---

# 🎯 Definition

`value()` এবং `pluck()`—দুটোই নির্দিষ্ট Column-এর Data Retrieve করার জন্য ব্যবহৃত হয়।

কিন্তু এদের Return Type এবং Use Case সম্পূর্ণ আলাদা।

---

# 📦 `value()`

`value()` শুধুমাত্র **একটি Column-এর প্রথম Value** Return করে।

```php
$email = Student::where('id', 1)
    ->value('email');
```

Generated SQL

```sql
SELECT email
FROM students
WHERE id = 1
LIMIT 1;
```

Return

```php
"emon@gmail.com"
```

---

# 📦 `pluck()`

`pluck()` একটি Column-এর **সব Value** Collection আকারে Return করে।

```php
$emails = Student::pluck('email');
```

Generated SQL

```sql
SELECT email
FROM students;
```

Return

```php
Illuminate\Support\Collection
```

Example

```php
[
    "emon@gmail.com",
    "rahim@gmail.com",
    "karim@gmail.com"
]
```

---

# 🔍 Difference

| `value()`                          | `pluck()`                   |
| ---------------------------------- | --------------------------- |
| Single Value                       | Multiple Values             |
| Returns String / Integer / Boolean | Returns Collection          |
| Uses `LIMIT 1`                     | Returns All Matching Values |
| Best for One Record                | Best for Lists              |
| Faster for Single Value            | Best for Multiple Values    |

---

# 💻 Example

## `value()`

```php
$email = Student::where('student_id', 1)
    ->value('email');

echo $email;
```

Output

```text
emon@gmail.com
```

---

## `pluck()`

```php
$emails = Student::pluck('email');

foreach ($emails as $email) {
    echo $email;
}
```

---

# 📌 Key-Value Pair

Dropdown বা Select Option তৈরির জন্য—

```php
$students = Student::pluck('name', 'id');
```

Return

```php
[
    1 => "Emon",
    2 => "Rahim",
    3 => "Karim"
]
```

---

# 🧠 Best Practice

## ✅ Use `value()`

যখন—

* একটি Email দরকার
* একটি Phone Number দরকার
* একটি Status দরকার
* একটি Price দরকার

Example

```php
$status = Student::where('id', 10)
    ->value('status');
```

---

## ✅ Use `pluck()`

যখন—

* Dropdown List
* Select Options
* Report
* Multiple Names
* Multiple IDs

Example

```php
$studentNames = Student::pluck('name');
```

---

# 📌 When to Use

| Situation         | Recommended |
| ----------------- | ----------- |
| Student Email     | `value()`   |
| Student Phone     | `value()`   |
| Product Price     | `value()`   |
| Category Dropdown | `pluck()`   |
| Student List      | `pluck()`   |
| Role Names        | `pluck()`   |

---

# ⚠️ Common Mistakes

## ❌ Mistake 1

```php
$email = Student::pluck('email');

echo $email;
```

`pluck()` Collection Return করে।

এটি সরাসরি String নয়।

---

## ✅ Correct

```php
$emails = Student::pluck('email');

foreach ($emails as $email) {
    echo $email;
}
```

---

## ❌ Mistake 2

```php
$email = Student::where('status', 'active')
    ->value('email');
```

যদি একাধিক Active Student থাকে, তাহলে শুধুমাত্র **প্রথম Record-এর Email** Return করবে।

---

## ✅ Correct

```php
$emails = Student::where('status', 'active')
    ->pluck('email');
```

---

# 📈 Performance Comparison

| Feature          | `value()`    | `pluck()`  |
| ---------------- | ------------ | ---------- |
| Return Type      | Scalar Value | Collection |
| Multiple Records | ❌ No         | ✅ Yes      |
| Memory Usage     | Lowest       | Low        |
| Performance      | ⭐⭐⭐⭐⭐        | ⭐⭐⭐⭐☆      |
| Production Ready | ✅            | ✅          |

---

# 🚀 Performance Tips

✅ শুধুমাত্র একটি Column-এর একটি Value দরকার হলে `value()` ব্যবহার করুন।

```php
$email = Student::where('id', 1)
    ->value('email');
```

✅ Dropdown বা Multiple Value-এর জন্য `pluck()` ব্যবহার করুন।

```php
$roles = Role::pluck('name', 'id');
```

❌ শুধু একটি Value দরকার হলে `pluck()->first()` ব্যবহার করবেন না।

```php
// ❌ Avoid
$email = Student::pluck('email')->first();
```

```php
// ✅ Better
$email = Student::value('email');
```

---

# 📝 Summary

* ✅ `value()` একটি মাত্র Value Return করে।
* ✅ `pluck()` একটি Column-এর সব Value Return করে।
* ✅ `value()` Scalar Return করে।
* ✅ `pluck()` Collection Return করে।
* ✅ Dropdown-এর জন্য `pluck()` সবচেয়ে ভালো।
* ✅ Single Value-এর জন্য `value()` ব্যবহার করুন।

---

# 💡 Quick Remember

```text
value()

Database
     │
     ▼
One Column
     │
     ▼
One Value
```

```text
pluck()

Database
     │
     ▼
One Column
     │
     ▼
Collection
```

---

# 🎯 Interview Question

### Question

নিচের কোনটি বেশি Efficient?

```php
Student::where('id', 1)->pluck('email')->first();
```

নাকি

```php
Student::where('id', 1)->value('email');
```

### Answer

যদি শুধুমাত্র **একটি Value** দরকার হয়, তাহলে **`value()`** ব্যবহার করুন।

কারণ `value()` সরাসরি Scalar Value Return করে, যেখানে `pluck()` আগে একটি Collection তৈরি করে, তারপর `first()` দিয়ে প্রথম Value বের করতে হয়।
