```pascal
// To get information about when a particular query has executed.

#mb_query(mb_addr := 123,
          mode := #mb_query.c.write.holding_reg,
          data_addr := 456,          
          data_ptr := #query_1);

// The if-statement bellow has to be put after the particular 
// query, and before the next query.    

IF #mb_query.Done THEN
    // Some action after a successfully query.
	          
ELSIF #mb_query.Error THEN
    // Some action faild a query.    

    // #mb_query.stat.status , gives more information about 
	// the error.         
	
    IF #mb_query.stat.error_comm THEN
        // Some particular action if communication error.
	End_if;
        
END_IF;
```
