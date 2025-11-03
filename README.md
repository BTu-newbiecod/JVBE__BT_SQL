# JVBE__BT_SQL

CODE:

```

CREATE TABLE Courses (
    course_id SERIAL PRIMARY KEY,
    course_name VARCHAR(100) NOT NULL,
    description TEXT,
    tuition_fee DECIMAL(10,2)
);


CREATE TABLE Instructors (
    instructor_id SERIAL PRIMARY KEY,
    full_name VARCHAR(100) NOT NULL,
    specialization VARCHAR(100),
    phone VARCHAR(20)
);


CREATE TABLE Students (
    student_id SERIAL PRIMARY KEY,
    full_name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    registration_date DATE DEFAULT CURRENT_DATE
);


CREATE TABLE Classes (
    class_id SERIAL PRIMARY KEY,
    schedule VARCHAR(100),
    instructor_id INT REFERENCES Instructors(instructor_id),
    course_id INT REFERENCES Courses(course_id)
);


CREATE TABLE Enrollments (
    enrollment_id SERIAL PRIMARY KEY,
    student_id INT REFERENCES Students(student_id) ON DELETE CASCADE,
    class_id INT REFERENCES Classes(class_id) ON DELETE CASCADE,
    enroll_date DATE DEFAULT CURRENT_DATE
);

```
