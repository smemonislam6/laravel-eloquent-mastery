# 🚀 Laravel Hack #02 — Model Object vs Collection

> Beginner Friendly | Laravel 13 | Bangla + English

---

# 🎯 Definition

## 📦 Model Object

যখন Eloquent একটি **Single Record** Return করে, তখন সেটি একটি **Model Object** হয়।

উদাহরণস্বরূপ, `Student::find(1)` একটি `Student` Model Object Return করে।

```php
$student = Student::find(1);
```

Return Type

```php
App\Models\Student
```

---

## 📚 Collection

যখন Eloquent **Multiple Records** Return করে, তখন সেটি একটি **Collection** Return করে।

উদাহরণস্বরূপ, `Student::all()` বা `Student::get()` একটি Collection Return করে।

```php
$students = Student::all();
```

Return Type

```php
Illuminate\Database\Eloquent\Collection
```

---

# 🔍 Difference

| Model Object           | Collection                          |
| ---------------------- | ----------------------------------- |
| Single Record          | Multiple Records                    |
| Return Type: `Student` | Return Type: `Collection`           |
| Object Property Access | Loop করে Access করতে হয়            |
| `find()`, `first()`    | `all()`, `get()`                    |
| `$student->name`       | `$students[0]->name` অথবা `foreach` |

---

# 💻 Example

## Model Object

```php
$student = Student::find(1);

echo $student->name;
echo $student->email;
```

Output

```text
Emon
emon@gmail.com
```

---

## Collection

```php
$students = Student::where('status', 'active')->get();

foreach ($students as $student) {
    echo $student->name;
}
```

---

# 📌 Access Difference

## Model Object

```php
$student = Student::find(1);

$student->name;
```

---

## Collection

```php
$students = Student::all();

$students[0]->name;
```

অথবা

```php
foreach ($students as $student) {
    echo $student->name;
}
```

---

# ⚡ Collection Methods

Collection-এর অনেক Helper Method আছে।

```php
$students->count();

$students->first();

$students->last();

$students->pluck('name');

$students->filter();

$students->map();

$students->sortBy('name');
```

এসব Method শুধুমাত্র Collection-এর জন্য।

---

# 🧠 Best Practice

✅ একটি নির্দিষ্ট Record দরকার হলে `find()` বা `first()` ব্যবহার করুন।

```php
$student = Student::find($id);
```

---

✅ একাধিক Record দরকার হলে `get()` ব্যবহার করুন।

```php
$students = Student::where('status', 'active')->get();
```

---

✅ Collection-এর উপর Loop চালান, Model Object-এর উপর নয়।

---

# 📌 When to Use

| Situation            | Use          |
| -------------------- | ------------ |
| একটি Student দরকার   | Model Object |
| একটি Teacher Profile | Model Object |
| Student List         | Collection   |
| Attendance Report    | Collection   |
| Dropdown Data        | Collection   |

---

# ⚠️ Common Mistakes

## ❌ Mistake 1

```php
$students = Student::get();

echo $students->name;
```

কারণ `get()` একটি Collection Return করে।

---

## ✅ Correct

```php
foreach ($students as $student) {
    echo $student->name;
}
```

---

## ❌ Mistake 2

```php
$student = Student::find(1);

foreach ($student as $item) {

}
```

কারণ `find()` একটি Model Object Return করে, Collection নয়।

---

# 📊 Quick Comparison

| Feature            | Model Object        | Collection           |
| ------------------ | ------------------- | -------------------- |
| Data               | Single Record       | Multiple Records     |
| Returned By        | `find()`, `first()` | `all()`, `get()`     |
| Loop Required      | ❌ No                | ✅ Yes                |
| Property Access    | `$student->name`    | `$students[0]->name` |
| Collection Methods | ❌ No                | ✅ Yes                |

---

# 📝 Summary

* ✅ Model Object = One Record
* ✅ Collection = Multiple Records
* ✅ `find()` ও `first()` Model Object Return করে
* ✅ `all()` ও `get()` Collection Return করে
* ✅ Collection-এর জন্য `foreach` এবং Collection Methods ব্যবহার করুন

---

# 💡 Quick Remember

```text
find()
first()
        │
        ▼
  Model Object
        │
        ▼
$student->name
```

```text
all()
get()
paginate()
        │
        ▼
 Collection
        │
        ▼
foreach (...)
```
