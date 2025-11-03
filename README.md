# JVBE__BT_SQL
CODE QUAN LY THU VIEN:

```
set search_path to library

create table Genres(
	genre_id serial primary key,
	genre_name varchar(100) not null,
	detail text
)
alter table Genres add unique(genre_name);

create table Books(
	book_id serial primary key,
	book_name varchar(100) not null,
	published_date date not null,
	stock_quantity int not null default 0,
	genre_id int,
	foreign key(genre_id) references Genres(genre_id)
)

alter table Books add check(stock_quantity>=0)

create table Authors(
	author_id serial primary key,
	author_name varchar(100) not null,
	biography text
)

create table Books_Authors(
	book_id int,
	author_id int,
	foreign key(book_id) references Books(book_id),
	foreign key(author_id) references Authors(author_id)
)
alter table Books_Authors add primary key (book_id, author_id)

create table Customers(
	customer_id serial primary key,
	customer_name varchar(100) not null,
	address varchar(150),
	birthday date,
	phone_number varchar(100) not null,
	registered_date date default current_date,
	status varchar(50) check(status in ('SUBCRIBED','UNSUBCRIBED'))
)
alter table Customers add unique(phone_number)

create table Forms(
	form_id serial primary key,
	borrowed_date date default current_date,
	customer_id int not null, foreign key(customer_id) references Customers(customer_id),
	status varchar(100) default 'borrow' check(status in ('borrow','back')),
	deadline date default (current_date +interval '30 days'),
	return_date date,
	fine decimal(10,2) default 0
)
alter table Forms add check(fine >=0)

create table Detail_Forms(
	book_id int, foreign key(book_id) references Books(book_id),
	form_id int, foreign key(form_id) references Forms(form_id) 
)
alter table Detail_Forms add primary key(book_id,form_id)

-- THEM INDEX CHO COT STATUS FORM 
create index idx_form_status on Forms(status);


```
