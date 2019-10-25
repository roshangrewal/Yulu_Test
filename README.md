# Yulu_Test

### Build a dummy database for Zomato with multiple tables and try to find an answer for the following question:

1. Write a SQL query to find the number of Zomato users /newline
#### Solution:  SELECT count(`id`) FROM `users`;  
<br />

2. Write a SQL query to find details of Zomato delivery Boy
##### Solution: SELECT * FROM `delivery_boys` WHERE id = 1; 

  delivery_boy_id should be in between 1 to 12. Because the total number of delivery boy entry in table is 12 and order is from 1 to 12.
<br />

3. Write a SQL query to find  the list of Zomato users who made more than 10 orders in a particular month
#### Solution:  SELECT u.id, u.name, u.mobile_no FROM `users` u, `orders` o WHERE u.id = o.user_id AND MONTH(`o`.`order_date_time`) = 10 AND YEAR(`o`.`order_date_time`) = YEAR(NOW()) GROUP BY `o`.`user_id` HAVING COUNT(`o`.`id`) > 10 ; 
<br />

4. Write a SQL query to find top 10 Zomato delivery Boy on basis of customer rating and time to deliver the item
#### Solution: (Partially Done, customer rating condition is not done) => Assuming  delivery time 30 minutes to deliver the item is good.
SELECT `delivery_boy_id`,`order_dispatched_date_time`,`order_received_date_time`, TIMESTAMPDIFF(MINUTE,`order_dispatched_date_time`,`order_received_date_time`) AS `total_minutes` FROM `orders` HAVING `total_minutes` < 30;
<br />

5. Write a SQL query to find the list of Zomato users who order food from the same restaurants more than 3 times in a week
#### Solution:  SELECT (SELECT `users`.`name` FROM `users` WHERE `users`.`id` = `orders`.`user_id`), `orders`.`restaurant_id`, count(`orders`.`id`) as `total_orders` FROM `orders` WHERE (WEEK(`orders`.`order_date_time`) = WEEK(NOW())) GROUP BY `orders`.`restaurant_id`, `orders`.`user_id` HAVING `total_orders` > 3 ;
<br />
