### Condition for execution

```pascal
// A query that has a condition for execution.
IF #conditon_of_exec_query THEN
    #mb_query(mb_addr := 123,
              mode := #mb_query.c.write.holding_reg,
              data_addr := 12345,              
              data_ptr := #query_data);
END_IF;
// When then number of queries changes with different plc-scan, 
// like above. Then the library gets a little "hiccup". If the 
// if-statement changes rapidly, then the example can break the
// whole modbus application.
```
