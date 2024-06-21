MySQL

~~~sql
SELECT 
    id, 
    CONCAT('SELECT * FROM t WHERE t.id = ''', id, ''';') AS generated_sql 
FROM 
    b;

~~~

