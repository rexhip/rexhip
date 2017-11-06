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
// following register. When the above situation is present, the SWAP_WORD 
// function needs to be used.

#mb_query(mb_addr := #mb_addr,               
          mode := #mb_query.c.read.holding_reg,
          data_addr := 123,               
          data_ptr := #static_tmp_var);                  
 
#value := SWAP_WORD(#static_tmp_var);
```

```pascal 
// In some situation both SWAP and SWAP_WORD need to be used.

#value := SWAP( SWAP_WORD( #tmp_var) );
```

How the data is stored in a device is usually described the
data sheet of the device.
