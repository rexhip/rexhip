```pascal
// For some modbus devices the dats is stored with little endian, not 
// big endian like Siemens PLC do. To solve this the swap function
// need to be utilize.

"mb_query"(unit := #unit,               
           fc := #mb.c.read.holding_reg,
           d_addr := 123,    
           d_len := 1,      
           data := #tmp_var,
           mb := #mb);                  

#value := SWAP(tmp_var);
```
 
```pascal 
"mb_query"(unit := #unit,               
           fc := #mb.c.read.holding_reg,
           d_addr := 123,    
           d_len := 2,      
           data := #tmp_var,
           mb := #mb);                  
 
$value := SWAP_WORD(tmp_var);
```
