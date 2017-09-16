// This is an advanced example which most users don't need to
// worry about. 
// 
// If there is a need of forcing some queries to be executed
// in a given order, then the example bellow should be followed.

CASE #state OF
    0:
        #mb_query(mb_addr := #mb_addr,
                  mode := #mb_query.c.write.holding_reg,
                  data_addr := 123,                  
                  data_ptr := #query_1);
        #state += BOOL_TO_SINT(#mb_query.stat.query_above AND #mb_query.stat.done);
        // "#mb_query.stat.query_above" is true if the query above
        // in the code just finished a query. (with or without error)        
    1:
        #mb_query(mb_addr := #mb_addr,
                  mode := #mb_query.c.write.holding_reg,
                  data_addr := 456,                   
                  data_ptr := #query_2);
        #state += BOOL_TO_SINT(#mb_query.stat.query_above AND #mb_query.stat.done);
    2:
        #mb_query(mb_addr := #mb_addr,
                  mode := #mb_query.c.read.holding_reg,
                  data_addr := 789,                   
                  data_ptr := #query_3);
        #state := SEL(G := #mb_query.stat.query_above AND #mb_query.stat.done, 
		              IN0 := #state, 
					  IN1 := 0);
ENdata_CASE;

