# 🚀 Laravel Hack: Model vs Eloquent

> Beginner Friendly | Laravel 13 

---

# 🎯 Definition

## 📦 Model

Model হলো Laravel-এর একটি PHP Class যা একটি Database Table-কে Represent করে।

একটি Model সাধারণত—

* Database Table-এর সাথে Mapping করে
* Business Logic ধারণ করে
* Relationships Define করে
* Eloquent-এর সব Feature ব্যবহার করতে পারে

Example

```php
class Student extends Model
{
    //
}
```

---

## ⚡ Eloquent

Eloquent হলো Laravel-এর **ORM (Object Relational Mapper)**।

এটি Model-এর মাধ্যমে Database-এর সাথে যোগাযোগ করে।

যখন আপনি লিখেন—

```php
Student::all();
```

তখন আসলে **Eloquent** SQL তৈরি করে Database থেকে Data নিয়ে আসে।

---

# 🔍 Difference

| Model                        | Eloquent                       |
| ---------------------------- | ------------------------------ |
| PHP Class                    | ORM (Object Relational Mapper) |
| Database Table Represent করে | Database Query তৈরি করে        |
| Relationships Define করে     | CRUD Operation পরিচালনা করে    |
| Business Logic রাখতে পারে    | SQL Automatically Generate করে |
| `Student`                    | `Student::where()`             |

---

# 💻 Example

## Model

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Student extends Model
{
    protected $fillable = [
        'name',
        'email',
    ];
}
```

---

## Eloquent

```php
$students = Student::all();
```

Generated SQL

```sql
SELECT * FROM students;
```

---

আরও Example

```php
Student::find(1);

Student::where('status', 'active')->get();

Student::create([
    'name' => 'Emon',
    'email' => 'emon@gmail.com'
]);
```

উপরের প্রতিটি Query **Eloquent** Execute করছে।

---

# 🧠 Best Practice

✅ প্রতিটি Database Table-এর জন্য একটি Model তৈরি করুন।

✅ Business Logic Model-এর মধ্যে রাখুন।

✅ Database Query করার জন্য Eloquent ব্যবহার করুন।

✅ Naming Convention Follow করুন।

---

# 📌 When to Use

| Situation                     | Use      |
| ----------------------------- | -------- |
| Database Table Represent করতে | Model    |
| Database থেকে Data আনতে       | Eloquent |
| Insert / Update / Delete      | Eloquent |
| Relationship Define করতে      | Model    |
| Query Filtering করতে          | Eloquent |

---

# ⚠️ Common Mistake

অনেকে মনে করেন—

> **Model এবং Eloquent একই জিনিস।**

❌ এটি ভুল।

বাস্তবে—

* **Model** হলো একটি PHP Class।
* **Eloquent** হলো সেই Model-এর মাধ্যমে Database-এর সাথে কাজ করার ORM।

---

# 📝 Summary

* ✅ Model = Database Table-এর Representation
* ✅ Eloquent = Database Query করার ORM
* ✅ Model ছাড়া Eloquent ব্যবহার করা যায় না
* ✅ Eloquent Model-এর মাধ্যমে Database-এর সাথে যোগাযোগ করে

---

# 💡 Quick Remember

```text
Database Table
      │
      ▼
    Model
      │
      ▼
   Eloquent ORM
      │
      ▼
   SQL Query
      │
      ▼
   Database
```
