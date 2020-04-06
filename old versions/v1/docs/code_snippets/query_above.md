
```pascal

// To get information about when a particular query has executed the 
// query_above boolian can be used.

"mb_query"(unit := 123,
           fc := #mb.c.write.holding_reg,
           d_addr := 456,
           d_len := #mb.c.auto_len,
           data := #query_1,
           mb := #mb);

IF #mb.stat.query_above THEN
    // This if-statement has to be put after the particular query, 
    // and before the next query.
    
    // Further, one can check the status of previous query    
    
    IF #mb.stat.done THEN
        ; // Some action after a successfully query.
    
    ELSIF #mb.stat.timeout THEN
        ; // Some other action if communication problems.
    
    ELSIF #mb.stat.error THEN
        ; // Or some action if other error problem.
        
        // #mb.stat.status , gives more information about the error
        // The error codes can be looked up in the help-manual,
        // check MB_MASTER for mosbus rtu, and for modbus tcp
        // check MB_CLIENT, TCON, TDISCON, TSEND and TRCV.
        
    END_IF;    

END_IF;

```
