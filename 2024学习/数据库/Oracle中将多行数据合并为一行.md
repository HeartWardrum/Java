使用wm_concat函数

例如：

~~~sql
select 
    risk_id, wm_concat(risk_rule) 
from risk_jour 
where risk_id='50010'
group by risk_id
~~~

