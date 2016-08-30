Lightweight Modbus Abstraction Layer Library.
---------------------------------------------
For Siemens S7-1200 and S7-1500 PLC's.

```
Author:   Ola Bjørnli
License:  MIT-license
Web:      http://mb.sn7.no
          http://github.com/olab84/sn7mb
```

The library extend on MB_MASTER and MB_CLIENT, the modbus blocks that comes along with 
TIA-portal. The library is not an attempt to reinvent the wheel, by doing what those 
blocks already do. Rather it's an attempt to expand the existing blocks, and to create 
a common clean API for what the library call "device blocks". (interface blocks)

```
// A modbus RTU example that illustrate the library. Support for modbus tcp is also included.

#mb_master_controller(
    hardware_id := "Local~CB_1241_(RS485)", 
    baud := 9600, // bps
    parity := true, // Enable even parity.
    timeout := T#500ms,   
    buffer_db_any := "modbus_rtu_buffer",  
    buffer_variant := "modbus_rtu_buffer",  
    mb := #mb ); // a udt that comes along with the library

// Query 1: Read holding registers.
"mb_query"(unit := 2,                 // Station address
           fc := #mb.fc.mode_read,    // Mode or function code.    
           d_addr := 40005,           // Register address
           d_len := 4,                // Length
           data := #resualt_data_1,
           mb := #mb); // same udt as on the controller
            
// Query 2 - Read input registers.
"mb_query"(unit := 4,                   
           fc := #mb.fc.read_input_reg, 
           d_addr := 123,               
           d_len := #mb.c.auto_len,     
           data := #resualt_data_2,
           mb := #mb); 
```

Key features:
 - Avoid global states, which make it possible to create reusable 
   device blocks, similar to proibus gsd-files. 
 - Advanced timeout handler that reduce idle time.  
 - Take care of executing the queries, one by one.
 - Logging capabilities for development and debugging.
 - Clean and readable API.  
 - Readable code still for application with hundreds of devices.
 - Store results inside optimized memory areas.
   
Requirements:
 - TIA-portal: v13, sp1, upd8 (or greater)
 - S7-1200: firmware version >= 4.1.3
 - S7-1500: not tested, but should work fine.
 
```
The software is not affiliated with Siemens AG
```  