### Case Study Questions: -
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



Q6. Which item was purchased first by the customer after they became a member?

Q7. Which item was purchased just before the customer became a member?

Q8. What is the total items and amount spent for each member before they became a member?

Q9. If each $1 spent equates to 10 points and sushi has a 2x points multiplier — how many points would each customer have?

Q10. In the first week after a customer joins the program (including their join date) they earn 2x points on all items, not just sushi — how many points do customer A and B have at the end of January?
