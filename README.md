Step 1: Problem Definition

Business Context: A Global e-commerce retailer that Sales Analytics in Retail industry.

Data Challenge.

The company has no visibility in its performance of individual regional sales or customer purchase behavior, which leads to low inventory allocation and generic marketing strategies. Sale data is dispersed and it's impossible to pinpoint best-selling products as well as endangered customer groups.

Expected Outcome.

Determine best-sellers by region/quarter, track sales trends via a moving average and separate clients by how frequently they make purchases to build targeted marketing initiatives and increase revenues 12% in the fiscal year ahead.

Step 2: Success Criteria

Define exactly 5 measurable goals:

1.Top 5 Products per Region/Quarter
 Function: RANK() OVER(PARTITION BY region, quarter ORDER BY sales DESC)
 Object: Find the top5 best selling products each region in every quarter.
 Metric: Rank of product in terms of sales.

2.Running Monthly Sales Totals
 Function: SUM(sales) OVER(PARTITION BY region ORDER BY month ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW )
 Objective: Sum total sales amount by month region wise.
 Metric: Running sales trend to monitor the increment in performance.

3.Month-over-Month Growth
 Function: LAG(sales, 1) OVER(PARTITION BY region ORDER BY month)
 Objective: To compare sales of the current month with the last month sales to see growth.
 Metric: % change in sales by region month-over-month.

4. Customer Quartiles
 Function: NTILE(4) OVER(ORDER BY total_spent DESC)
 Goal: Split customers into quartiles based on total spending.
 Metric: Top 25% high-value customers compared to bottom 25% low-spending customers.

5. 3-Month Moving Averages
 Function: AVG(sales) OVER(ORDER BY month ROWS BETWEEN 2 PRECEDING AND CURRENT ROW)
 Goal: Smooth out volatility in sales by providing a rolling 3-month average.
 Metric: Trend analysis for short-term sales stability or volatility.

Step 3: Database Schema & ER Diagram.
Database Schema
Tables
- `customers`: Customer info (customer_id, name, region)
- `products`: Product catalog (product_id, name, category)
- `transactions`: Sales records (transaction_id, customer_id, product_id, sale_date, amount)

 ER Diagram

 <img width="1100" height="510" alt="Screenshot 2025-09-28 181552" src="https://github.com/user-attachments/assets/ab00de08-482d-4eab-9f82-e065e947caf5" />

 Relationships that are in ER Diagram,
customers → transactions:
One customer can have many transactions (1-to-many).  
Foreign key: transactions.customer_id references customers.customer_id  
products → transactions:  
One product can appear in many transactions (1-to-many).  
Foreign key: transactions.product_id references products.product_id






