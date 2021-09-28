# MySQL cheat sheet
## Process JSON array with objects
* Create Procedure
```SQL
CREATE PROCEDURE `dorepeat`(p1 varchar(5000))
BEGIN
SET  @indx = 0;
REPEAT
        SET @txt = JSON_EXTRACT(p1, CONCAT("$[", @indx, "]"));
        
        SELECT JSON_EXTRACT(@txt, '$.id') as Id, JSON_EXTRACT(@txt, '$.name') as Name;
        
        SET @indx = @indx + 1;
        UNTIL @indx = JSON_LENGTH(p1)
END REPEAT;
END
```
* Execute
```SQL
call dorepeat('[{"id":1,"name":"t1"},{"id":2,"name":"t2"},{"id":3,"name":"t3"}]');
```

## Resources
* [MySQL docs](https://dev.mysql.com/doc/refman/8.0/en/json.html)
* [Repeat example](https://stackoverflow.com/questions/34681925/iterate-through-json-in-mysql-query/48809401)
