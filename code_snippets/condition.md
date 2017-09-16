// A query that has a condition for execution.
IF #conditon_of_exec_query THEN
    #mb_query(mb_addr := 1,
              mode := #mb_query.c.write.holding_reg,
              data_addr := 12345,              
              data_ptr := #query_data);
END_IF;
// When there is a plc-scan where the number of queries changes, the
// library gets a little "hiccup". If the if-statement changes rapidly,
// then the example above won't work, and it will also interfere with
// other queries bellow. 
