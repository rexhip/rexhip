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
blocks already do extraordinary. Rather it's an attempt to expand the existing blocks,
and to create a common clean API for "device blocks".

```
// A modbus RTU example that illustrate the library. Support for modbus tcp is also included.

#mb_master_controller(
    hardware_id := "Local~CB_1241_(RS485)", 
    baud := 9600, // bps
    parity := true, // Enable even parity.
    timeout := T#500ms,   
    buffer_db_any := "modbus_rtu_buffer",  
    buffer_variant := "modbus_rtu_buffer",  
    mb := #mb ); // a udt that comes with the library

// Query 1: Read holding registers.
"mb_query"(unit := 2,                     // device address
           fc := #mb.fc.read_holding_reg, // function code
           d_addr := 55,                  // data address
           d_len := 10,                   // data length
           data := #resualt_data_1,
           mb := #mb); // same udt as on the controller
            
// .-------.-------.-------------.-------------.- . . . . ---.-------------.		   
// | unit  |  fc   |   d_addr    |    d_len    |     data    |     CRC     |
// '-------'-------'-------------'-------------'--- . . . . -'-------------'		   
//
// - Parameters of the query above correlate to the fields in the telegram.  
// - The result of the query will be stored inside the variable connected to 
//   "data". Because "data" is variant it can store any kind of data type, 
//   including arrays and complex structures. 
// - "d_addr" is the value that will be sent in the modbus telegram. To access 
//   holding register number 55 as in the example, input 55, and not 40056. 

// Query 2 - Read input registers.
"mb_query"(unit := 4,                   // device address
           fc := #mb.fc.read_input_reg, // function code
           d_addr := 123,               // data address
           d_len := #mb.c.auto_len,     // data length
           data := #resualt_data_2,
           mb := #mb); // same udt as above		  
```

Key features:
 - Take care of executing the queries, one by one.
 - Logging capabilities for development and debugging.
 - Avoid global states, which make it possible to create reusable 
   device blocks, similar to proibus gsd-files. 
 - Clean and readable API.  
 - Readable code still for application with hundreds of devices.
 - Advanced timeout handler that reduce idle time.  
 - Store results inside optimized memory areas.
   
Requirements:
 - TIA-portal: v13, sp1, upd8 (or greater)
 - S7-1200: firmware version >= 4.1.3
 - S7-1500: not tested
 
```
The software is not affiliated with Siemens AG
```  