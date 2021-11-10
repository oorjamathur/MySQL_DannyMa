## Case Study Questions: -

![Danny's Diner](https://ejournalz.com/wp-content/uploads/2019/05/ramen_3000.jpg)

Link of the case study: https://8weeksqlchallenge.com/case-study-1/

<b> Q1. What is the total amount each customer spent at the restaurant? </b>

 <i> select customer_id, sum(price) from sales, menu where sales.product_id=menu.product_id group by customer_id; </i>
 
 ![ans1](https://github.com/oorjamathur/MySQL_DannyMa/blob/main/Case%20Study%201%20Solutions/cs1_q1.PNG)


<b> Q2. How many days has each customer visited the restaurant? </b>

<i> select customer_id, count(distinct(order_date)) as no_of_days from sales group by customer_id; </i>

 ![ans2](https://github.com/oorjamathur/MySQL_DannyMa/blob/main/Case%20Study%201%20Solutions/cs1_q2.PNG)


<b> Q3. What was the first item from the menu purchased by each customer? </b>

<i> select customer_id, product_id, order_date from (select *, rank() over (partition by customer_id order by order_date) as r from sales) as temp where r=1 group by customer_id; </i>

![ans3](https://github.com/oorjamathur/MySQL_DannyMa/blob/main/Case%20Study%201%20Solutions/cs1_q3.PNG)

<b> Q4. What is the most purchased item on the menu and how many times was it purchased by all customers? </b>

<i> with cte as (select product_id as pid, count(product_id) as x from sales group by product_id order by x desc limit 1)
   
 select customer_id, count(product_id) from sales, cte where cte.pid=sales.product_id group by customer_id; </i>
    
![ans4](https://github.com/oorjamathur/MySQL_DannyMa/blob/main/Case%20Study%201%20Solutions/cs1_q4.PNG)

<b> Q5. Which item was the most popular for each customer? </b>

<i> select customer_id, product_id, count from (select customer_id, product_id, count, rank() over (partition by customer_id order by count desc) as r from (select customer_id, 
product_id,count(*) as count from sales group by customer_id, product_id) as t) as tab where r=1 group by customer_id; </i>

![ans5](https://github.com/oorjamathur/MySQL_DannyMa/blob/main/Case%20Study%201%20Solutions/cs1_q5.PNG)

<b> Q6. Which item was purchased first by the customer after they became a member? </b>

<i> select customer_id, product_id, order_date from (select *, rank() over (partition by customer_id order by order_date) as r from sales) as temp where r=1 group by customer_id; </i>


![ans6](https://github.com/oorjamathur/MySQL_DannyMa/blob/main/Case%20Study%201%20Solutions/cs1_q6.PNG)


<b> Q7. Which item was purchased just before the customer became a member? </b>

<i> select customer_id, product_id from (select sales.customer_id, product_id, order_date, join_date, rank() over (partition by customer_id order by order_date desc) as r from sales, members where sales.customer_id=members.customer_id and sales.order_date<members.join_date) as tab where r=1 group by customer_id; </i>
 

![ans7](https://github.com/oorjamathur/MySQL_DannyMa/blob/main/Case%20Study%201%20Solutions/cs1_q7.PNG)

<b> Q8. What is the total items and amount spent for each member before they became a member? </b>
 
<i> select sales.customer_id, count(sales.product_id) as total_items_purchased, sum(price) as total_amt_spent from sales, menu, members where sales.customer_id=members.customer_id and sales.product_id=menu.product_id and order_date<join_date group by sales.customer_id; </i>
 

![ans8](https://github.com/oorjamathur/MySQL_DannyMa/blob/main/Case%20Study%201%20Solutions/cs1_q8.PNG)


<b> Q9. If each $1 spent equates to 10 points and sushi has a 2x points multiplier — how many points would each customer have? </b>
 
<i> select customer_id, sum(points) from (select *, case when product_name = "sushi" then 20*price else price*10 end as points from (select customer_id, product_name, price from sales, menu where sales.product_id=menu.product_id) as t) as temptab group by customer_id; </i>
 

![ans9](https://github.com/oorjamathur/MySQL_DannyMa/blob/main/Case%20Study%201%20Solutions/cs1_q9.PNG)


<b> Q10. In the first week after a customer joins the program (including their join date) they earn 2x points on all items, not just sushi — how many points do customer A and B have at the end of January? </b>

<i> select sales.customer_id, sales.order_date, sales.product_id, members.join_date, menu.product_name, menu.price, case when product_name="sushi" or order_date>=join_date then price*20 when order_date<join_date then price*10 end as points from sales, members, menu where sales.product_id=menu.product_id and sales.customer_id=members.customer_id; </i>
 

![ans10](https://github.com/oorjamathur/MySQL_DannyMa/blob/main/Case%20Study%201%20Solutions/cs1_q10.PNG)
 
## Credits: Danny Ma
