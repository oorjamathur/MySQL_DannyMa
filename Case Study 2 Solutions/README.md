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

5. How many of each type of pizza was delivered?
6. How many Vegetarian and Meatlovers were ordered by each customer?
7. What was the maximum number of pizzas delivered in a single order?
8. For each customer, how many delivered pizzas had at least 1 change and how many had no changes?
9. How many pizzas were delivered that had both exclusions and extras?
10. What was the total volume of pizzas ordered for each hour of the day?
11. What was the volume of orders for each day of the week?


## B. Runner and Customer Experience
1. How many runners signed up for each 1 week period? (i.e. week starts 2021-01-01)
2. What was the average time in minutes it took for each runner to arrive at the Pizza Runner HQ to pickup the order?
3. Is there any relationship between the number of pizzas and how long the order takes to prepare?
4. What was the average distance travelled for each customer?
5. What was the difference between the longest and shortest delivery times for all orders?
6. What was the average speed for each runner for each delivery and do you notice any trend for these values?
7. What is the successful delivery percentage for each runner?


## C. Ingredient Optimisation
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


## D. Pricing and Ratings
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

## E. Bonus Questions
If Danny wants to expand his range of pizzas - how would this impact the existing data design? Write an INSERT statement to demonstrate what would happen if a new Supreme pizza with all the toppings was added to the Pizza Runner menu?
