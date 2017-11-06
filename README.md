Rexhip - Extended modbus library for Siemens PLC's.
---------------------------------------------------

Key features:
 - Makes it easy to create and split a program in to reusable «station blocks» (interface blocks).
 - Station blocks can easily be reused and combined in new programs.
 - A clean API, helps to cut engineering time.
 - Reduce idle time, by skipping queries that has led to recurring timeouts. (Retries will be done occasionally)
 - Logging features for development and debugging.
 - The library extend on MB_MASTER and MB_CLIENT, the modbus blocks that comes along with TIA-portal.
 - The software use little memory and cpu-time, important for S7-1200.
 - Free under the MIT-license.

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
// - The library will take care of executing the queries, 
//   one by one. 
```
   
Requirements:
 - Software: TIA-portal: v14, sp1, Upd 2
 - Hardware: S7-1200: fw >= 4.2   
             S7-1500: fw >= 2.0   (currently only modbus tcp)
 - (For older fw. use v1 "_old_version_v1")
   
Quick starter guide:
 - Download the latest release. (https://github.com/olab84/rexhip/releases)
 - Start a new project in TIA-portal, and then add new PLC.
 - Localise "External Source files" in the tree structure and import the files inside the lib-folder of the downloaded zip-file.
 - Select the imported files, right click them and choose "Generate blocks from source".
 - Study the start examples and customize the code for your modbus device. 
 
 ```
 Author:   Ola Bjørnli
 ```
 
 ![.](http://p.sn7.no/piwik.php?idsite=2&rec=1)
