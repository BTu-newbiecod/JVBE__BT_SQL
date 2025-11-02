# JVBE__BT_SQL
CODE SESSION 2 KHA:

```
Set search_path to library

create table Books(
	book_id serial primary key,
	title varchar(100) not null,
	author varchar(50) not null,
	published_year int,
	price decimal(10,2)
)

 \c ten database :chuyen den database do
\dn :xem tat ca cac schema
\d tenschme.ten table
```
