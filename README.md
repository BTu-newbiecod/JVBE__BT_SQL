# JVBE__BT_SQL

```
set search_path to baitap

create table Products(
	product_id serial primary key,
	product_name varchar(100) unique not null,
	category varchar(100) not null
);

insert into Products(product_name,category)
values
('Laptop Dell','Electronics'),
('IPhone 15','Electronics'),
('Ban hoc go','Furniture'),
('Ghe xoay','Furniture')

create table Orders(
	order_id int primary key,
	product_id int,
	quantity int default 1,
	total_price decimal(10,2) not null,
	foreign key(product_id) references Products(product_id)
);

insert into Orders
values
(101,1,2,2200),
(102,2,3,3300),
(103,3,5,2500),
(104,4,4,1600),
(105,1,1,1100)

select p.category,
	sum(o.total_price) as total_sale,
	sum(o.quantity) as total_quantity
from Products as p
join orders as o
	on p.product_id=o.product_id
group by p.category
having sum(o.total_price)>2000
order by sum(o.total_price) desc
```
