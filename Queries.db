-- Retrieving top-selling medicines per region

SELECT m.name, COUNT(oi.id) AS total_sold, u.region 
FROM orders o 
JOIN order_items oi ON o.id = oi.order_id
JOIN medicines m ON oi.medicine_id = m.id
JOIN users u ON o.user_id = u.id
GROUP BY m.name, u.region
ORDER BY total_sold DESC;

-- Calculating inventory turnover rate
  
SELECT m.name, 
       (SUM(oi.quantity) / SUM(i.quantity)) AS turnover_rate
FROM order_items oi
JOIN medicines m ON oi.medicine_id = m.id
JOIN inventory i ON m.id = i.medicine_id
GROUP BY m.name;

-- Identifying frequent Customers Based on Purchase History

SELECT u.name, u.email, COUNT(o.id) AS order_count
FROM users u
JOIN orders o ON u.id = o.user_id
GROUP BY u.id
ORDER BY order_count DESC
LIMIT 10;
