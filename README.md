# -pl-sql-window-functions--BAZIGA-Caleb---NKURANGA-
SELECT 
    DATE_FORMAT(o.order_date, '%Y-%m') AS month,
    m.name AS menu_item,
    SUM(o.amount) AS total_sales,
    RANK() OVER (PARTITION BY DATE_FORMAT(o.order_date, '%Y-%m') 
                 ORDER BY SUM(o.amount) DESC) AS item_rank
FROM orders o
JOIN menu_items m ON o.item_id = m.item_id
GROUP BY month, m.name
ORDER BY month, item_rank;
