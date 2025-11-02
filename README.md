# JVBE__BT_SQL

SESSION 2 KHA 2:

```
set search_path to university;

create table Students(
	student_id serial primary key,
	first_name varchar(50) not null,
	last_name varchar(50) not null,
	birth_date date,
	email varchar(100) not null unique
);

create table Courses(
	course_id serial primary key,
	course_name varchar(100) not null,
	credits int
);

create table Enrollments(
	enrollment_id serial primary key,
	student_id int,
	course_id int,
	enroll_date date default current_date,

	foreign key(student_id) references Students(student_id),
	foreign key(course_id) references Courses(course_id)
)
```
