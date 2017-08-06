// This is an advanced example which most users don't need to
// worry about. 
// 
// If there is a need of forcing some queries to be executed
// in a given order, then the example bellow should be followed.

CASE #state OF
    0:
        "mb_query"(unit := #unit,
                   fc := #mb.c.write.holding_reg,
                   d_addr := 123,
                   d_len := #mb.c.auto_len,
                   data := #query_1,
                   mb := #mb);
        #state := #state + BOOL_TO_SINT(#mb.stat.query_above AND #mb.stat.done);
        // "#mb.stat.query_above" is true if the query above
        // in the code just finnished a query. (with or without error)        
    1:
        "mb_query"(unit := #unit,
                   fc := #mb.c.write.holding_reg,
                   d_addr := 456,
                   d_len := #mb.c.auto_len,
                   data := #query_2,
                   mb := #mb);
        #state := #state + BOOL_TO_SINT(#mb.stat.query_above AND #mb.stat.done);
    2:
        "mb_query"(unit := #unit,
                   fc := #mb.c.read.holding_reg,
                   d_addr := 789,
                   d_len := #mb.c.auto_len,
                   data := #query_3,
                   mb := #mb);
        #state := SEL(G := #mb.stat.query_above AND #mb.stat.done, IN0 := #state, IN1 := 0);
END_CASE;

