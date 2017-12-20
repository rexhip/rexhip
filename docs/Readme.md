### Extended modbus library for Siemens PLC's.

 - A clean and simple api that makes it easy to split a program into reusable FB for each modbus station.
 - «Station blocks», or SB's can easily be combined in new programs. A application with 100 devices, can be developed within 10 minutes when there exist SB's.
 - The library includes many free SB's ready to be used. (and growing...)
 - Reduce idle time, by skipping queries that has led to recurring timeouts, retries will be done occasionally.
 - Logging features for development and debugging.
 - Extend on the modbus blocks that comes along in TIA-portal, it isn't an attempt to reinvent the wheel, but to extend it.
 - Help share the bus efficient between the devices.
 - Data can be stored with optimized data access on.
 - Use little memory.
 - Free under the MIT-license. (docs/License.txt)
 
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


- Author: Ola Bjørnli - [Contact](http://sn7.no/contact/rexhip)
- This library has been included in [Siemens Open libarary](http://openplclibrary.com) 
![.](http://p.sn7.no/piwik.php?idsite=2&rec=1) <!-- Visitor statistics -->
