```pascal
// For some modbus devices, when two regisers are combined into one,
// the data is stored as little endian, not big endian like Siemens 
// PLC does. To solve this, the SWAP function needs to be utilized.

"mb_query"(unit := #unit,               
           fc := #mb.c.read.holding_reg,
           d_addr := 123,    
           d_len := 1,      
           data := #static_tmp_var,
           mb := #mb);                  

#value := SWAP(#static_tmp_var);
```
 
```pascal 
// For other device, when two registers are combined, the least significant 
// word is stored first and the most significant word is stored in the 
// following register. When the above situation is present, the SWAP_WORD 
// function needs to be used.

"mb_query"(unit := #unit,               
           fc := #mb.c.read.holding_reg,
           d_addr := 123,    
           d_len := 2,      
           data := #static_tmp_var,
           mb := #mb);                  
 
#value := SWAP_WORD(#static_tmp_var);
```

```pascal 
// The most confusing situation is when both SWAP and SWAP_WORD 
// need to be used.

#value := SWAP( SWAP_WORD( #tmp_var) );
```

How the data is stored in a device is usually described the
datasheet of the device.
