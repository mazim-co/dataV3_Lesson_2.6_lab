-- Get release years.

select distinct release_year from sakila.film;

-- Get all films with ARMAGEDDON in the title.

select * from sakila.film_list
where title like '%ARMAGEDDON%';

-- Get all films which title ends with APOLLO.

select * from sakila.film_list
where title like '%APOLLO';

-- Get 10 the longest films.

select * from sakila.film
order by length desc
limit 10;

-- How many films include Behind the Scenes content?

select count(*) from sakila.film
where special_features like '%Behind the Scenes%';

-- Drop column picture from staff.
alter table sakila.staff drop column picture;

-- A new person is hired to help Jon. Her name is TAMMY SANDERS, and she is a customer. Update the database accordingly.

select * from sakila.customer
where first_name = 'TAMMY' and Last_name = 'SANDERS';

insert into saklia.staff(first_name, last_name, email, address_id, store, username)
values('TAMMY', 'SANDERS', 'tammy_sanders@sakilacustomer.com', 79, 2, 'tammy' )

-- Add rental for movie "Academy Dinosaur" by Charlotte Hunter from Mike Hillyer at Store 1. You can use current date for the rental_date column in the rental table. Hint: Check the columns in the table rental and see what information you would need to add there. You can query those pieces of information. For eg., you would notice that you need customer_id information as well. To get that you can use the following query:

-- get customer_id
select customer_id from sakila.customer where first_name = 'CHARLOTTE' and last_name = 'HUNTER';
-- expected customer_id = 130
-- get film_id
select film_id from sakila.film where title = 'ACADEMY DINOSAUR';
-- expected film_id = 1
-- get inventory_id
select inventory_id from sakila.inventory where film_id = 1;
-- expected inventory_id = 1
-- get staff_id
select * from sakila.staff;
-- expected staff_id = 1
insert into sakila.rental(rental_date, inventory_id, customer_id, staff_id)
values (curdate(), 1, 130, 1);

-- select customer_id from sakila.customer

-- where first_name = 'CHARLOTTE' and last_name = 'HUNTER';

-- Use similar method to get inventory_id, film_id, and staff_id.

-- Delete non-active users, but first, create a backup table deleted_users to store customer_id, email, and the date for the users that would be deleted. Follow these steps:

    Check if there are any non-active users
    Create a table backup table as suggested
    Insert the non active users in the table backup table
    Delete the non active users from the table customer