use information_schema;
select * from information_schema.columns where table_schema ='ntemergency'  and table_name = 'EMERGENCY_CRANE';
SELECT * FROM `SYS_USER`   

 select * from information_schema.columns where table_schema ='codenai'  and table_name = 'SYS_USER'  
 
 
  select * from information_schema.columns where table_schema ='ntemergency'  and table_name = 'SYS_USER' 
	
	

	
	
	SELECT
	TABLE_NAME 表名,
	TABLE_COMMENT '表注解' 
FROM
	INFORMATION_SCHEMA.TABLES 
WHERE
	table_schema = 'ntemergency' 
	AND (TABLE_COMMENT LIKE '%用户%' or table_name like '%U%');