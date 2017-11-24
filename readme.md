Rexhip - Extended modbus library for Siemens PLC's.
---------------------------------------------------
 - Makes it easy to create and split a program in to reusable «station blocks» (SB).
 - Station blocks can easily be reused and combined in new programs.
 - A clean API, helps to cut engineering time.
 - Reduce idle time, by skipping queries that has led to recurring timeouts, retries will be done occasionally.
 - Logging features for development and debugging.
 - The library extend on the modbus blocks that comes along with TIA-portal.
 - The software use little memory and cpu-time, important for S7-1200.
 - Free under the MIT-license. (docs/LICENSE.txt)
 - More then 50 SB's included.

```pascal
// A simple modbus RTU example. 
// (Support for modbus TCP is also available)

#mb_master_ctrl(hardware_id := "Local~CB_1241_(RS485)", 
                baud := 19200, // bps                
                mb_query := #mb_query ); 

#mb_query(mb_addr := #mb_addr,                  
          mode := #mb_query.c.read.input_reg, 
          data_addr := 13,                      
          data_ptr := #resault_data_1);                   

#mb_query(mb_addr := #mb_addr,                 
          mode := #mb_query.c.write.holding_reg, 
          data_addr := 55,                            
          data_ptr := #resault_data_2);
		  
// - The result will be stored in the connected variable 
//   of data_ptr. The variable can be any data types, 
//   including arrays and udt's.
// - Length will be calculated automatically. 
// - The library will take care of executing the 
//   queries, one by one. 
// - Queries belonging to one device can be grouped together 
//   into one FB, creating a reusable station block.
```
    
 
 Author:   Ola Bjørnli - [Contact](http://sn7.no/contact/rexhip)
 
![.](http://p.sn7.no/piwik.php?idsite=2&rec=1) <!-- Visitor statistics -->
