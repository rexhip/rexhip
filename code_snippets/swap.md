```pascal
// For some modbus devices, when two regiser is combined in to one,
// the dats is stored as little endian, not big endian like Siemens 
// PLC do. To solve this the swap function need to be utilize.

"mb_query"(unit := #unit,               
           fc := #mb.c.read.holding_reg,
           d_addr := 123,    
           d_len := 1,      
           data := #static_tmp_var,
           mb := #mb);                  

#value := SWAP(#static_tmp_var);
```
 
```pascal 
// For other devices when two registeres are combined, the least significant 
// word is stored first and the most significant word is stored in the 
// following register. In those situation the swap_word function need to 
// be used.

"mb_query"(unit := #unit,               
           fc := #mb.c.read.holding_reg,
           d_addr := 123,    
           d_len := 2,      
           data := #static_tmp_var,
           mb := #mb);                  
 
#value := SWAP_WORD(#static_tmp_var);
```

```pascal 
// The most confustion situation is when both swap and swap_word 
// need to be used.

#value := SWAP( SWAP_WORD( #tmp_var) );
```

How the data is stored in a device should be described the
datasheet of the device.
