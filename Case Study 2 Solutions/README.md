![Pizza Runner](http://images2.fanpop.com/images/photos/7300000/Slice-of-Pizza-pizza-7383219-1600-1200.jpg)

Link of the case study: https://8weeksqlchallenge.com/case-study-2/

## A. Pizza Metrics

<b> 1. How many pizzas were ordered? </b>

<i> select customer_id, sum(c) from (select customer_id, pizza_id, count(*) as c from customer_orders group by customer_id, pizza_id) as temp; </i>

![soln1](https://github.com/oorjamathur/MySQL_DannyMa/blob/main/Case%20Study%202%20Solutions/cs2_q1.PNG)

<b> 2. How many unique customer orders were made? </b>

<i> select customer_id, sum(c) as unique_orders from (select customer_id, pizza_id, count(*) as c from customer_orders group by customer_id, pizza_id) as temp group by customer_id; </i>

![soln2](https://github.com/oorjamathur/MySQL_DannyMa/blob/main/Case%20Study%202%20Solutions/cs2_q2.PNG)

<b> 3. How many successful orders were delivered by each runner? </b>

<i> select runner_id, count(*) as successful_runs from runner_orders where cancellation="" or cancellation is null group by runner_id; </i>

![soln3](https://github.com/oorjamathur/MySQL_DannyMa/blob/main/Case%20Study%202%20Solutions/cs2_q3.PNG)

<b> 4. How many of each type of pizza was delivered? </b>

<i> select pizza_id, count(*) as no_of_deliveries from customer_orders, runner_orders where customer_orders.order_id=runner_orders.order_id and (cancellation="" or cancellation is null) group by pizza_id; </i>

![soln4](https://github.com/oorjamathur/MySQL_DannyMa/blob/main/Case%20Study%202%20Solutions/cs2_q4.PNG)

<b> 5. How many Vegetarian and Meatlovers were ordered by each customer? </b>

<i> select customer_id, pizza_name, count(*) from (select customer_id, customer_orders.pizza_id, pizza_name from customer_orders, pizza_names where customer_orders.pizza_id=pizza_names.pizza_id) as t group by customer_id, pizza_name; </i>

![soln5](https://github.com/oorjamathur/MySQL_DannyMa/blob/main/Case%20Study%202%20Solutions/cs2_q5.PNG)

<b> 6. What was the maximum number of pizzas delivered in a single order? </b>

<i>select order_id, count(pizza_id) as count from (select customer_orders.order_id, customer_orders.pizza_id from customer_orders, runner_orders where customer_orders.order_id=runner_orders.order_id and (cancellation is null or cancellation="")) as temp group by order_id order by count desc limit 1;</i>

![soln6](https://github.com/oorjamathur/MySQL_DannyMa/blob/main/Case%20Study%202%20Solutions/cs2_q6.PNG)

<b> 7. For each customer, how many delivered pizzas had at least 1 change and how many had no changes? </b>

<i>select customer_id, case when sum_changes=0 then "no changes" else "at least one change" end as is_changed from (select customer_id, sum(changes) as sum_changes from (select customer_id, case when (exclusions="" or exclusions is null) and (extras is null or extras="") then 0 else 1 end as changes from customer_orders, runner_orders where customer_orders.order_id=runner_orders.order_id and (cancellation is null or cancellation="")) as temp group by customer_id) as temp_table;</i>

![soln7](https://github.com/oorjamathur/MySQL_DannyMa/blob/main/Case%20Study%202%20Solutions/cs2_q7.PNG)

<b> 8. How many pizzas were delivered that had both exclusions and extras? </b>

<i>select count(*) from customer_orders, runner_orders where runner_orders.order_id=customer_orders.order_id and (exclusions!="" and exclusions is not null) and (extras!="" and extras is not null) and (cancellation is null or cancellation="");</i>

![soln8](https://github.com/oorjamathur/MySQL_DannyMa/blob/main/Case%20Study%202%20Solutions/cs2_q8.PNG)

<b> 9. What was the total volume of pizzas ordered for each hour of the day? </b>

<i>select hour, count(*) as no_of_pizzas from (select *, hour(order_time) as hour from customer_orders) as temp group by hour;</i>

![soln9](https://github.com/oorjamathur/MySQL_DannyMa/blob/main/Case%20Study%202%20Solutions/cs2_q9.PNG)

<b> 10. What was the volume of orders for each day of the week? </b>

<i>select week, count(*) as no_of_pizzas from (select *, week(order_time) as week from customer_orders) as temp group by week;</i>

![soln10](https://github.com/oorjamathur/MySQL_DannyMa/blob/main/Case%20Study%202%20Solutions/cs2_q10.PNG)



## B. Runner and Customer Experience (TODO)
1. How many runners signed up for each 1 week period? (i.e. week starts 2021-01-01)
2. What was the average time in minutes it took for each runner to arrive at the Pizza Runner HQ to pickup the order?
3. Is there any relationship between the number of pizzas and how long the order takes to prepare?
4. What was the average distance travelled for each customer?
5. What was the difference between the longest and shortest delivery times for all orders?
6. What was the average speed for each runner for each delivery and do you notice any trend for these values?
7. What is the successful delivery percentage for each runner?


## C. Ingredient Optimisation (TODO)
1. What are the standard ingredients for each pizza?
2. What was the most commonly added extra?
3. What was the most common exclusion?
4. Generate an order item for each record in the customers_orders table in the format of one of the following:
- Meat Lovers
- Meat Lovers - Exclude Beef
- Meat Lovers - Extra Bacon
- Meat Lovers - Exclude Cheese, Bacon - Extra Mushroom, Peppers
5. Generate an alphabetically ordered comma separated ingredient list for each pizza order from the customer_orders table and add a 2x in front of any relevant ingredients
- For example: "Meat Lovers: 2xBacon, Beef, ... , Salami"
6. What is the total quantity of each ingredient used in all delivered pizzas sorted by most frequent first?


## D. Pricing and Ratings (TODO)
1. If a Meat Lovers pizza costs $12 and Vegetarian costs $10 and there were no charges for changes - how much money has Pizza Runner made so far if there are no delivery fees?
2. What if there was an additional $1 charge for any pizza extras?
- Add cheese is $1 extra
3. The Pizza Runner team now wants to add an additional ratings system that allows customers to rate their runner, how would you design an additional table for this new dataset - generate a schema for this new table and insert your own data for ratings for each successful customer order between 1 to 5.
4. Using your newly generated table - can you join all of the information together to form a table which has the following information for successful deliveries?
- customer_id
- order_id
- runner_id
- rating
- order_time
- pickup_time
- Time between order and pickup
- Delivery duration
- Average speed
- Total number of pizzas
5. If a Meat Lovers pizza was $12 and Vegetarian $10 fixed prices with no cost for extras and each runner is paid $0.30 per kilometre traveled - how much money does Pizza Runner have left over after these deliveries?

## E. Bonus Questions (TODO)
If Danny wants to expand his range of pizzas - how would this impact the existing data design? Write an INSERT statement to demonstrate what would happen if a new Supreme pizza with all the toppings was added to the Pizza Runner menu?
