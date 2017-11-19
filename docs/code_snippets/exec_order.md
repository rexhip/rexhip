```pascal
// If the execution need to be forced to a given 
// order, then the example bellow should be followed.

CASE #state OF
    
    0:  // 1st query
        #mb_query(mb_addr := #mb_addr,
                  mode := #mb_query.c.write.holding_reg,
                  data_addr := 123,                  
                  data_ptr := #query_1);
        #state += BOOL_TO_SINT(#mb_query.done);
        // "#mb_query.done" is true if the query above
        // in the code just finished a query. (without error)        
    
    1:  // 2nd query
        #mb_query(mb_addr := #mb_addr,
                  mode := #mb_query.c.write.holding_reg,
                  data_addr := 456,                   
                  data_ptr := #query_2);
        #state += BOOL_TO_SINT(#mb_query.done);
    
    2:  // 3rd query
        #mb_query(mb_addr := #mb_addr,
                  mode := #mb_query.c.read.holding_reg,
                  data_addr := 789,                   
                  data_ptr := #query_3);
        #state += BOOL_TO_SINT(#mb_query.done);
	
    else
        #state := 0; 		      
ENdata_CASE;
```
