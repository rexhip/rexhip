Automatic data_len
------------------

The liberay is able to determine the data_len parmeter automatically for holding and input register. This feature only works digital input and outputs, when the number of bits adds up to whole bytes.

If data_len i set manually for one query, then it need to be set back to auto in the following query.

```pascal
#mb_query.mb_addr := __MB_ADDR__;

// A query where data_len is set manually.
#mb_query(mode := #mb_query.c.write.digital_output,
          data_addr := __REGISTER__,          
          data_len := 2, 
          data_ptr := #array_with_two_bools); 

// Data length is set back to auto, by passing zero.
#mb_query(mode := #mb_query.c.read.holding_reg,
          data_addr := __REGISTER__,      
          data_len := #mb_query.c.auto_len,
          data_ptr := #read_query_2); 
```
