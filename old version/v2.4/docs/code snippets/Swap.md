```pascal
// For some modbus devices, when two registers are combined into one,
// the data is stored as little endian, not big endian like Siemens 
// PLC does. To solve this, the SWAP function needs to be utilized.

#mb_query(mb_addr := #mb_addr,               
          mode := #mb_query.c.read.holding_reg,
          data_addr := 123,               
          data_ptr := #static_tmp_var);                  

#value := SWAP(#static_tmp_var);
```
 
```pascal 
// For other device, when two registers are combined, the least significant 
// word is stored first and the most significant word is stored in the 
// following register. When this is the case, the ROR-function needs 
// to be used.

#mb_query(mb_addr := #mb_addr,               
          mode := #mb_query.c.read.holding_reg,
          data_addr := 123,               
          data_ptr := #static_tmp_var);                  
 
#value := ROR(IN := #static_tmp_var, N := 16);
```

```pascal 
// In some situation both SWAP and ROR need to be used.

#value := SWAP( ROR(IN := #tmp_var, N := 16) );
```

How the data is stored, is usually described in the data sheet of the particular device.
