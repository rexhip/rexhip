```pascal
// If the execution need to be forced to a given 
// order, then the example bellow can be followed.

CASE #state OF
    
    0:  // 1st query
        #mb_query(mb_addr := #mb_addr,
                  mode := #mb_query.c.write.holding_reg,
                  data_addr := 123,                  
                  data_ptr := #query_1);
        #state += BOOL_TO_SINT(#mb_query.done);
        // «#mb_query.done» is set true when the query above done 
	// successfully. When next query is executed, «#mb_query.done»
	// is set back false.
    
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
	IF #mb_query.done THEN
            #state := 0;
	END_IF;
END_CASE;

// 4th query, this query is executed three times as often 
// as the queries above.
#mb_query(mb_addr := #mb_addr,
          mode := #mb_query.c.read.input_reg,
          data_addr := 1234,                   
          data_ptr := #query_4 );
```
