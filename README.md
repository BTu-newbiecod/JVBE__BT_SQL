# JVBE__BT_SQL
CODE SESSION 4:
```
create table Customers(
    customer_id serial primary key,
    full_name varchar(100),
    email varchar(100) unique,
    phone varchar(100),
    city varchar(100),
    join_date date default current_date
);

create table Products(
    product_id serial primary key,
    product_name varchar(100) not null unique,
    category varchar(100),
    price decimal(10,2),
    stock_quantity int
);

create table Orders(
    order_id serial primary key,
    customer_id int,
    order_date date,
    total_amount decimal(10,2),
    status varchar(100),
    foreign key(customer_id) references Customers(customer_id)
);

insert into Customers
values
(1,'van a','a@gmail.com','012341','hanoi'),
(2,'van b','b@gmail.com','012342','bacninh'),
(3,'van c','c@gmail.com','012343','nghean'),
(4,'van d','d@gmail.com','012344','thanhoa'),
(5,'van e','e@gmail.com','012345','hanoi'),
(6,'van f','f@gmail.com','012346','vungtau'),
(7,'van g','g@gmail.com','012347','bacgiang'),
(8,'van h','h@gmail.com','012348','hanoi'),
(9,'van i','i@gmail.com','012349','hanoi'),
(10,'van j','j@gmail.com','0123410','hanoi');



insert into Products (product_name, category, price, stock_quantity)
values
    ('iPhone 14', 'Electronics', 25000.00, 50),
    ('Samsung Galaxy S23', 'Electronics', 22000.00, 40),
    ('MacBook Air M2', 'Electronics', 32000.00, 30),
    ('Dell XPS 13', 'Electronics', 28000.00, 20),
    ('Sony Headphones', 'Electronics', 3500.00, 100),

    ('Men T-Shirt', 'Clothing', 400.00, 200),
    ('Women Dress', 'Clothing', 800.00, 150),
    ('Jeans Pants', 'Clothing', 700.00, 180),
    ('Jacket', 'Clothing', 1200.00, 100),
    ('Sneakers', 'Clothing', 1500.00, 90),

    ('Microwave Oven', 'Home Appliances', 2500.00, 60),
    ('Air Conditioner', 'Home Appliances', 12000.00, 25),
    ('Washing Machine', 'Home Appliances', 9500.00, 30),
    ('Vacuum Cleaner', 'Home Appliances', 3200.00, 50),
    ('Electric Kettle', 'Home Appliances', 600.00, 100);

insert into Orders (customer_id, order_date, total_amount, status)
values
    (1, '2025-10-15', 25000.00, 'Pending'),
    (2, '2025-10-16', 22000.00, 'Shipped'),
    (3, '2025-10-17', 800.00, 'Delivered'),
    (4, '2025-10-18', 1200.00, 'Cancelled'),
    (5, '2025-10-19', 9500.00, 'Processing'),
    (6, '2025-10-20', 3500.00, 'Returned'),
    (7, '2025-10-21', 32000.00, 'Completed'),
    (8, '2025-10-22', 1500.00, 'Failed');

update Products
set price = price + (10.0/100.0)*price
where category = 'Electronics';

update Orders
set status='Confirmed'
where status='Pending';

delete
from Customers
where customer_id not in(
    select o.customer_id
    from Orders as o
);

-- TRUY VAN

--TIM KHACH HANG THEO TEN
select c.customer_id, full_name, email, phone, city, join_date, customer_id, full_name, email, phone, city, join_date
from Customers as c
where full_name ilike '%a';

--Lọc sản phẩm theo khoảng giá (sử dụng BETWEEN)
select product_id, product_name, category, price, stock_quantity, product_id, product_name, category, price, stock_quantity
from Products as p
where p.price between 1000 and 10000;

--Đếm số khách hàng theo thành phố (DISTINCT + COUNT)
select city,count(*) as "so_luong"
from Customers as c
group by  city
order by so_luong,city;

--Sản phẩm chưa được bán (NOT EXISTS)
create table Order_Details (
   order_detail_id serial primary key,
   order_id int not null,
   product_id int not null,
   quantity int not null check (quantity > 0),
   unit_price decimal(10,2) not null,
   foreign key(order_id) references Orders(order_id),
   foreign key(product_id) references Products(product_id)
);

insert into Order_Details (order_id, product_id, quantity, unit_price)
values
-- Order 1 (customer_id = 1)
(1, 1, 1, 27500.00),   -- iPhone 14 (đã tăng 10%)
(1, 5, 2, 3850.00),    -- Sony Headphones

-- Order 2
(2, 2, 1, 24200.00),   -- Galaxy S23
(2, 10, 1, 1500.00),   -- Sneakers

-- Order 3
(3, 7, 1, 800.00),     -- Women Dress
(3, 9, 1, 1200.00),    -- Jacket

-- Order 4
(4, 8, 2, 700.00),     -- Jeans Pants

-- Order 5
(5, 12, 1, 12000.00),  -- Air Conditioner

-- Order 6
(6, 5, 1, 3850.00),    -- Sony Headphones

-- Order 7
(7, 3, 1, 35200.00),   -- MacBook Air M2
(7, 11, 1, 2500.00),   -- Microwave Oven

-- Order 8
(8, 6, 2, 400.00);     -- Men T-Shirt

insert into Products (product_name, category, price, stock_quantity)
values
    ('Gaming Keyboard', 'Electronics', 1800.00, 70),
    ('Smartwatch Pro', 'Electronics', 5500.00, 60),
    ('Curtains', 'Home Appliances', 900.00, 40);


select product_id, product_name, category, price, stock_quantity, product_id, product_name, category, price, stock_quantity
from Products as p
where not exists(
    select 1
    from Order_Details as d
    where d.product_id=p.product_id
)
```
