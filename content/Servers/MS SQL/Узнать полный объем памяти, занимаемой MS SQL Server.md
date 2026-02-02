SELECT cntr_value/1024 as Mb  
FROM  
master..sysperfinfo  
WHERE  
counter_name = 'Total Server Memory (KB)'