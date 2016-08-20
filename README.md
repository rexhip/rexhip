Lightweight Modbus Abstraction Layer Library.
---------------------------------------------
For Siemens S7-1200 and S7-1500 PLC's.

```
Author:   Ola Bjørnli
License:  MIT-license
Web:      http://mb.sn7.no
          http://github.com/olab84/sn7mb
```

All though the new plc-series from Siemens has built in support for modbus. The opinion of the author is that modbus can be done slightly easier with an abstraction layer on top of mb_master or mb_client. This apply especially if there is a lot of modbus devices connected to one bus.

```
// A modbus RTU example that illustrate the library. Support for modbus tcp is also included.

#mb_rtu_controller(
    hardware := "Local~CB_1241_(RS485)", 
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
// - Parameters of the FC above correlate to the fields in the telegram.  
// - "data" is a inOut variant parameter where the query result will be stored. 
//   The parameter can be any kind of data type, including arrays and complex
//   structures. The datatype should match the datatype of the registers being 
//   queried.   
// - "d_addr" is the value that will be sent in the modbus telegram. To access 
//   holding register number 55 as in the example, just put 55, and not 40056. 

// Query 2 - Read input registers.
"mb_query"(unit := 4,                   // device address
           fc := #mb.fc.read_input_reg, // function code
           d_addr := 123,               // data address
           d_len := #mb.c.auto_len,     // data length
           data := #resualt_data_2,
           mb := #mb); // same udt as above		  
```

Key features.
 - Take care of executing the queries one by one.
 - Logging capabilities for development and debugging.
 - Avoid global states, to make reusable code.
 - Clean and readable user API.
 - Good timeout handling to avoiding delay on the bus for other queries.

Requirements:
 - TIA-portal: v13, sp1, upd8 (or greater)
 - S7-1200: firmware version >= 4.1.3

```
The software is not affiliated with Siemens AG
```  