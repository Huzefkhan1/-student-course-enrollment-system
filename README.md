# Student Course Enrollment Management System
## 📌 Project Objective
This project addresses a real-world challenge faced by a training institute: as the number of enrolled students keeps growing, tracking student details, course enrollments, instructor assignments, and completion status manually through Excel becomes increasingly difficult and error-prone.

This SQL-based system replaces manual tracking with a structured relational database that makes it easy to manage and query student, course, instructor, and enrollment data.

## 🎯 Business Problem
> In a training institute, data is maintained in an Excel file. As the number of students increases, manually analyzing and tracking this data becomes difficult.

## 🗄️ Database Schema

The database (`SQLPROJECT`) consists of 4 core tables:

| Table | Description |
|---|---|
| `students` | Stores student personal details — name, gender, age, city, email, phone, joining date |
| `instructors` | Stores instructor details — name, department, years of experience |
| `courses` | Stores course details — name, duration, fee, and the instructor teaching it |
| `enrollments` | Bridge table linking students to courses — tracks enrollment date, completion status, and marks 

## 🔍 Key Queries

**1. Courses with fee greater than 5000**
```sql
select count(*)
from courses
where Fee > 5000;
```

**2. Number of students enrolled in each course**
```sql
select c.CourseName, count(e.EnrollmentID) as total_students
from courses c
join enrollments e on c.CourseID = e.CourseID
group by c.CourseName;
```

**3. Students with a specific completion status (e.g., Completed / Ongoing)**
```sql
select s.studentname, c.coursename, e.Comletionstatus
from students s
join enrollments e on s.student_id = e.StudentsID
join courses c on c.courseid = e.courseid
where e.Comletionstatus = "Completed";
```

**4. Revenue generated per course**
```sql
select c.coursename, count(e.StudentsID) * c.fee as revenue
from enrollments e
join courses c on e.courseid = c.courseid
group by c.coursename, c.fee;

## 🛠️ Tools Used
- MySQL
- MySQL Workbench

## 📈 What I Learned
Working through this project reinforced how critical **consistent naming conventions** are in relational database design. Several early bugs came from mismatched column names across tables (e.g., `student_id` vs `StudentsID`, `instructorID` vs `instructorsID`) causing foreign key and join failures. This taught me to always verify column names with `DESC tablename;` before writing joins, and to keep naming consistent from the start to avoid cascading errors later.

