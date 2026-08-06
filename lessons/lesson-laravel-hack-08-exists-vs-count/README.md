# 🚀 Laravel Hack #08 — `exists()` vs `count()`

> Beginner Friendly | Laravel 13

---

# 🎯 Definition

`exists()` এবং `count()`—দুটোই Database-এ Record আছে কিনা তা জানতে ব্যবহার করা যায়।

কিন্তু এদের উদ্দেশ্য (Purpose), Return Type এবং Performance এক নয়।

অনেক Developer শুধু Record আছে কিনা Check করার জন্য `count()` ব্যবহার করেন।

❌ এটি সবসময় Best Practice নয়।

---

# 📦 `exists()`

`exists()` Check করে **কমপক্ষে একটি Record আছে কিনা**।

```php id="a7h3xk"
$exists = Student::where('email', 'emon@gmail.com')
    ->exists();
```

Generated SQL

```sql id="m8q2vp"
SELECT EXISTS(
    SELECT *
    FROM students
    WHERE email = 'emon@gmail.com'
) AS exists;
```

Return

```php id="z4qn61"
true
```

অথবা

```php id="e8s5hf"
false
```

---

# 📦 `count()`

`count()` Matching Record-এর **মোট সংখ্যা** Return করে।

```php id="q2m7nd"
$total = Student::where('status', 'active')
    ->count();
```

Generated SQL

```sql id="w1r9lg"
SELECT COUNT(*)
FROM students
WHERE status = 'active';
```

Return

```php id="b6j4po"
25
```

---

# 🔍 Difference

| `exists()`                | `count()`                   |
| ------------------------- | --------------------------- |
| Record আছে কিনা Check করে | মোট Record Count করে        |
| Returns `true` / `false`  | Returns Integer             |
| Stops at First Match      | Counts All Matching Records |
| Faster                    | তুলনামূলক ধীর               |
| Best for Existence Check  | Best for Total Count        |

---

# 💻 Example

## `exists()`

```php id="t5j8yn"
if (
    Student::where('student_id', $id)->exists()
) {
    echo "Student Found";
}
```

---

## `count()`

```php id="k9v2rh"
$totalStudents = Student::count();

echo $totalStudents;
```

Output

```text id="h3n7qb"
1500
```

---

# 📌 Login Example

Check Email Exists

```php id="n2p6wy"
$emailExists = User::where('email', $email)
    ->exists();
```

এখানে `count()` ব্যবহার করার দরকার নেই।

---

# 📌 Report Example

Active Students

```php id="u4r8mc"
$total = Student::where('status', 'active')
    ->count();
```

এখানে `count()` ব্যবহার করাই সঠিক।

---

# 🧠 Best Practice

## ✅ Use `exists()`

যখন—

* Email Exists কিনা
* Username Exists কিনা
* Student Exists কিনা
* Duplicate Check
* Validation
* Authorization Check

Example

```php id="v0m5zk"
if (Student::where('email', $email)->exists()) {

}
```

---

## ✅ Use `count()`

যখন—

* Dashboard Statistics
* Reports
* Total Students
* Total Teachers
* Total Orders
* Total Payments

Example

```php id="7xq4cl"
$totalOrders = Order::count();
```

---

# 📌 When to Use

| Situation            | Recommended |
| -------------------- | ----------- |
| Email Exists?        | `exists()`  |
| Username Exists?     | `exists()`  |
| Student Exists?      | `exists()`  |
| Total Students       | `count()`   |
| Total Orders         | `count()`   |
| Dashboard Statistics | `count()`   |

---

# ⚠️ Common Mistakes

## ❌ Mistake 1

```php id="d8q3hy"
if (
    Student::where('email', $email)
        ->count() > 0
) {

}
```

এটি কাজ করবে, কিন্তু Performance-এর দিক থেকে Best নয়।

---

## ✅ Better

```php id="j6n4vt"
if (
    Student::where('email', $email)
        ->exists()
) {

}
```

---

## ❌ Mistake 2

```php id="f9m2qx"
$total = Student::exists();
```

`exists()` মোট Record সংখ্যা দেয় না।

---

## ✅ Correct

```php id="s8l7zr"
$total = Student::count();
```

---

# 📈 Performance Comparison

| Feature             | `exists()` | `count()` |
| ------------------- | ---------- | --------- |
| Return Type         | Boolean    | Integer   |
| Stops Early         | ✅ Yes      | ❌ No      |
| Counts All Records  | ❌          | ✅         |
| Performance         | ⭐⭐⭐⭐⭐      | ⭐⭐⭐⭐☆     |
| Best for Validation | ✅          | ❌         |
| Best for Reports    | ❌          | ✅         |

---

# 🚀 Performance Tips

✅ শুধু Record আছে কিনা Check করতে `exists()` ব্যবহার করুন।

```php id="x5p9rc"
Student::where('email', $email)
    ->exists();
```

✅ Dashboard বা Analytics-এর জন্য `count()` ব্যবহার করুন।

```php id="x2n7qa"
Student::count();
```

❌ Existence Check-এর জন্য `count() > 0` ব্যবহার করা Avoid করুন।

```php id="e4v8yt"
// ❌ Avoid
Student::where('email', $email)
    ->count() > 0;
```

```php id="b1m3zk"
// ✅ Better
Student::where('email', $email)
    ->exists();
```

---

# 📝 Summary

* ✅ `exists()` Record আছে কিনা Check করে।
* ✅ `count()` মোট Record সংখ্যা Return করে।
* ✅ `exists()` Boolean Return করে।
* ✅ `count()` Integer Return করে।
* ✅ Existence Check-এর জন্য `exists()` ব্যবহার করুন।
* ✅ Reports ও Statistics-এর জন্য `count()` ব্যবহার করুন।

---

# 💡 Quick Remember

```text id="c8t5yn"
exists()

Database
     │
     ▼
Found?
     │
     ▼
true / false
```

```text id="g3m8vr"
count()

Database
     │
     ▼
Count All
     │
     ▼
25
```

---

# 🎯 Interview Question

### Question

নিচের কোনটি বেশি Efficient?

```php id="v6j2ph"
Student::where('email', $email)
    ->count() > 0;
```

নাকি

```php id="r9k4xm"
Student::where('email', $email)
    ->exists();
```

### Answer

যদি শুধু **Record আছে কিনা** জানতে চান, তাহলে **`exists()`** ব্যবহার করুন।

কারণ `exists()` প্রথম Matching Record পেলেই Query শেষ করতে পারে, কিন্তু `count()` সব Matching Record গণনা করে। তাই Existence Check-এর জন্য `exists()` বেশি Efficient এবং Laravel-এর Recommended Approach।
