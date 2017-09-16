// A query that has a condition for execution.
IF #conditon_of_exec_query THEN
    "mb_query"(unit := 1,
               fc := #mb.c.write.holding_reg,
               d_addr := 12345,
               d_len := #mb.c.auto_len,
               data := #query_data,
               mb := #mb);
END_IF;
// When there is a plc-scan where the number of queries changes, the
// library gets a little "hiccup". If the if-statement changes rapidly,
// then the example above won't work, and it will also interfere with
// other queries bellow. 
