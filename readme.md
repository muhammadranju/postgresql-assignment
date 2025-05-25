## What is PostgreSQL?

PostgreSQL (Postgres) হলো একটি জনপ্রিয় open-source relational database system, যা SQL ও JSON দুই ধরনের data সাপোর্ট করে। ACID-compliant হওয়ায় data safe থাকে। এতে আছে:

- Custom data types, functions, extensions
- উন্নত indexing (B-tree, GIN, ইত্যাদি)
- Full-text search
- Replication ও high availability
- PL/pgSQL সহ অনেক ভাষায় stored procedures
- JSON ও geospatial support

1986 সালে UC Berkeley-তে শুরু, আজ এটি active open-source community দ্বারা maintain হয়।

---

## Purpose of a Database Schema in PostgreSQL

Schema হলো database-এর ভেতরে logical folder, যা table, view ইত্যাদি organize করে।

এর উদ্দেশ্য:

- Structure manage করা
- একই নামের object আলাদা রাখা (namespace)
- Security ও permission control
- Multi-tenancy support
- Logical grouping

ডিফল্টভাবে public schema থাকে, তবে বড় প্রজেক্টে custom schema ভালো।

---

## Difference Between VARCHAR and CHAR

| বৈশিষ্ট্য | CHAR                     | VARCHAR            |
| --------- | ------------------------ | ------------------ |
| Length    | Fixed (e.g., 10)         | Variable           |
| Storage   | Full length নেয়          | যতটুকু লাগে ততটুকু |
| Padding   | শেষে space দেয়           | Padding দেয় না     |
| Use Case  | Fixed data (e.g., codes) | Variable data      |

**সংক্ষেপে:** Fixed হলে CHAR, না হলে VARCHAR।

---

## LIMIT এবং OFFSET কী?

- `LIMIT`: কতটি row return করবে।
- `OFFSET`: কতটি row skip করবে।

**উদাহরণ:**

```sql
SELECT * FROM customers ORDER BY id LIMIT 10 OFFSET 20;
```

এখানে প্রথম ২০টি বাদ দিয়ে পরের ১০টি row দেখাবে।

**নোট:** ORDER BY না দিলে row-এর order নিশ্চিত না।

---

## UPDATE দিয়ে Data পরিবর্তন

`UPDATE` টেবিলের ডেটা পরিবর্তনের জন্য ব্যবহৃত হয়।

**Syntax:**

```sql
UPDATE table_name
SET column = value
WHERE condition;
```

**উদাহরণ:**

```sql
UPDATE students SET age = 16 WHERE name = 'John Doe';
```

- `WHERE` না দিলে সব row আপডেট হয়।
- Expression দিয়ে মান পরিবর্তন সম্ভব (`salary = salary * 1.05`)।
- `RETURNING` দিয়ে পরিবর্তিত row দেখা যায়।
