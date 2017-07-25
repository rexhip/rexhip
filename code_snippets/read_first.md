```pascal
// Sometimes only one bit in a word need to be manupulated, without touching the 
// other bits, bellow is an example how that can be achieved.


if #static_read_done then
  
  // Manupulating only bit 5 and 11
  #static_var.X5 := __TRUE_OR_FALSE__ ;
  #static_var.X11 := __TRUE_OR_FALSE__ ;
  
  "mb_query"(unit := __UNIT__,               
             fc := #mb.c.write.holding_reg,
             d_addr := __REGISTER__,    
             d_len := 1,      
             data := #static_var,
             mb := #mb); 
else
  "mb_query"(unit := __UNIT__,               
             fc := #mb.c.read.holding_reg,
             d_addr := __REGISTER__,    
             d_len := 1,      
             data := #static_var,
             mb := #mb);   
             
  if #mb.stat.query_above and #mb.stat.done then
      #static_var := true;
  end_if;

end_if;

```

