### Extended modbus library for Siemens PLC's.

The library makes it possible to split a program into reusable function blocks for each modbus device. This blocks can later be reused and combined in new programs. Together with a clean and simple api this speed up devopment significantly. Other features include:

 - Reduce idle time, by skipping queries that has led to recurring timeouts, retries will be done occasionally.
 - More then 70 ready to use device profiles (Station blocks), similarities to profibus gsd-files.
 - Logging features for development and debugging.
 - Extend on the modbus blocks that comes along in TIA-portal, it isn't an attempt to reinvent the wheel, but to extend functionality.
 - Help share the bus efficient between the devices.
 - Data can be stored with optimized data access on.
 - Use little memory.
 - Free under the [MIT-license](/docs/License.txt).

```pascal
// A simple modbus RTU example. 
// (Support for modbus TCP is also available)

#mb_rtu1500_ctrl(hardware_id := "Local~CB_1241_(RS485)", 
                baud := 19200, // bps                
                mb_query := #mb_query ); 

//  Use mb_rtu1200_ctrl for S7-1200

#mb_query(mb_addr := 1,                  
          mode := #mb_query.c.read.input_reg, 
          data_addr := 123,                      
          data_ptr := #resault_data_1);                   

#mb_query(mb_addr := 1,                 
          mode := #mb_query.c.read.holding_reg, 
          data_addr := 456,                            
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


#### Station block (SB) example 
This six lines of code bellow and the variable definition (not shown) is all that is needed to read the data from the a MAG 6000 device.

```pascal
// Siemens - SITRANS MAG 6000

"mb_station_block_header"(sb := #sb, mb_query := #mb_query);
#mb_query.mb_addr := #mb_addr;
	
#mb_query.mode := #mb_query.c.read.holding_reg;
#mb_query(data_addr := 2999, data_ptr := #flow);
#mb_query(data_addr := 3016, data_ptr := #totalizer);
	
"mb_station_block_footer"(sb := #sb, mb_query := #mb_query);

// - #flow is a struct that actually contain two variables. 
// - #mb_addr is a input 
// - #mb_query is a inOut on the block. 
// - #sb is a udt that come along with the library, with 
//   common information for the device.
```


#### Another station block example 
This SB can be combined with the one above, and any others in the library. It's also fine to have more instaces of one SB in the same program. New queries can be added without changing anything in existing program. 

```pascal
// Telemecanique (Schneider) - Altivar 21 inverter - VFD (AC-drive)

"mb_station_block_header"(sb := #sb, mb_query := #mb_query);
#mb_query.mb_addr := #mb_addr;

#mb_query.mode := #mb_query.c.read.holding_reg;
#mb_query(data_addr := 16#fd00, data_ptr := #read1);
#mb_query(data_addr := 16#fe45, data_ptr := #read2);
#mb_query(data_addr := 16#fe91, data_ptr := #read3_alarm);
#mb_query(data_addr := 16#fe79, data_ptr := #read4_alarm2);
#mb_query(data_addr := 16#FC90, data_ptr := #read5_trip_code);

#write1.ref := REAL_TO_UINT(#ref * 100);
#write1.cmd.x10_Run := #ref <> 0;
#mb_query.mode := #mb_query.c.write.holding_reg;
#mb_query(data_addr := 16#fa00, data_ptr := #write1);

"mb_station_block_footer"(sb := #sb, mb_query := #mb_query);
```

#### Modbus tcp example 

```pascal
#ip[1] := 192;
#ip[2] := 168;
#ip[3] := 1;
#ip[4] := 2;
#mb_tcp_ctrl(interface := "Local~PROFINET_interface_1",
             conn_id := 123,
             ip_addr := #ip,
             tcp_port := 502,
             timeout := T#2s,
             mb_query := #mb_query);

#mb_query(mb_addr := 255,
          mode := #mb_query.c.read.holding_reg,
          data_addr := 123,
          data_ptr := #resault_data_1);

#mb_query(mb_addr := 255,
          mode := #mb_query.c.read.holding_reg,
          data_addr := 456,
          data_ptr := #resault_data_2);
	  
// - Unlimited number of queries can be added.
// - The same station blocks created for rtu can also be used 
//   for tcp. This is convenient when a tcp-rtu-gateway is used.
#telemecanique_altivar(mb_addr := 255, mb_query := #mb_query);

```

- Author: Ola Bjørnli - [Contact](http://sn7.no/contact/rexhip)
- The library is part of [Siemens Open libarary](http://openplclibrary.com) 
