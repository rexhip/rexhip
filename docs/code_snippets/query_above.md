
```pascal

// This API maybe deprecated.

// To get information about when a particular query has executed the 
// query_above boolean can be used.

#mb_query(mb_addr := 123,
          mode := #mb_query.c.write.holding_reg,
          data_addr := 456,          
          data_ptr := #query_1);

IF #mb_query.stat.query_above THEN
    // This if-statement has to be put after the particular query, 
    // and before the next query.
    
    // Further, one can check the status of previous query    
    
    IF #mb_query.stat.done THEN
        ; // Some action after a successfully query.
    
    ELSIF #mb_query.stat.err_comm THEN
        ; // Some other action if communication problems.
    
    ELSIF #mb_query.stat.error THEN
        ; // Or some action if other error problem.
        
        // #mb_query.stat.status , gives more information about the 
		// error. The error codes can be looked up in the help-manual,
        // check MB_MASTER for mosbus rtu, and for modbus tcp
        // check MB_CLIENT
        
    END_IF;    

END_IF;

```
