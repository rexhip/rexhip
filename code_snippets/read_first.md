```pascal
// Sometimes only some bits in a word need to be manipulated, without touching the 
// other bits, bellow is an example how that can be achieved.

#mb_query.mb_addr := __mb_addr__,         
#mb_query.data_addr := __REGISTER__,             

if #static_write then // (Initially false)
  
   // Manipulating only bit 5 and 11
   #static_var.X5 := __TRUE_OR_FALSE__ ;
   #static_var.X11 := __TRUE_OR_FALSE__ ;
  
   #mb_query(mode := #mb_query.c.write.holding_reg,                          
             data_ptr := #static_var); 

else // read the register before write to the same one.
   #mb_query(mode := #mb_query.c.read.holding_reg,             
             data_ptr := #static_var);
  
   // Has query above been executed successfully?
   if #mb_query.stat.query_above and #mb_query.stat.done then
       #static_write := true; 
   end_if;

end_if;

```

