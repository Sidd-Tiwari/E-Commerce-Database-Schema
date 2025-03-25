-- Checking performance of a query

EXPLAIN ANALYZE 
SELECT m.name, COUNT(oi.id) AS total_sold
FROM orders o 
JOIN order_items oi ON o.id = oi.order_id
JOIN medicines m ON oi.medicine_id = m.id
GROUP BY m.name
ORDER BY total_sold DESC;

-- Indexes to  improve Query performance

CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_orders_user ON orders(user_id);
CREATE INDEX idx_medicine_name ON medicines(name);
CREATE INDEX idx_inventory_medicine ON inventory(medicine_id);

-- Retrieving Top-Selling Medicines Per Region

SELECT m.name, COUNT(oi.id) AS total_sold, u.region 
FROM orders o 
JOIN order_items oi ON o.id = oi.order_id
JOIN medicines m ON oi.medicine_id = m.id
JOIN users u ON o.user_id = u.id
GROUP BY m.name, u.region
ORDER BY total_sold DESC
LIMIT 10; 

-- Calculating Inventory Turnover Rate Efficiently

SELECT m.name, 
       (SUM(oi.quantity) / NULLIF(SUM(i.quantity), 0)) AS turnover_rate
FROM order_items oi
JOIN medicines m ON oi.medicine_id = m.id
JOIN inventory i ON m.id = i.medicine_id
GROUP BY m.name
HAVING turnover_rate IS NOT NULL;
