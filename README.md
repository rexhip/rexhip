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

Key features:
 - Avoid global states, which make it possible to create reusable device blocks. 
 - Clean and readable API.  
 - Advanced timeout handler that reduce idle time.  
 - Take all care of executing the queries, one by one. Sophisticated bus sharing 
   mechanism between devices.
 - Logging capabilities for development and debugging.
 - Possible to create readable code still for application with 
   hundreds of modbus devices.
 - Store results inside optimized memory areas.

```
// A modbus RTU example that illustrate the library. 
// (Support for modbus tcp is also included).

#mb_master_controller(
    hardware_id := "Local~CB_1241_(RS485)", 
    baud := 9600, // bps
    parity := true, // Enable even parity.
    timeout := T#500ms,   
    buffer_db_any := "modbus_rtu_buffer",  
    buffer_variant := "modbus_rtu_buffer",  
    mb := #mb ); // a udt that comes along with the library

// Instances of device blocks for ABB Aqua master 3	
#abb_aquaMaster_3_instance_1(unit := 1, mb := #mb);
#abb_aquaMaster_3_instance_2(unit := 2, mb := #mb);

// Instances of device blocks for Siemens PAC3200 
#siemens_PAC3200_instance_1(unit := 3, mb := #mb);
#siemens_PAC3200_instance_2(unit := 4, mb := #mb);


// -----------------------------------------------------------------------
// Device block for: ABB - AquaMaster 3 - Electromagnetic flowmeter

"mb_device_header"(device := #device_udt, mb := #mb);

"mb_query"(unit := #unit,                // Station address.
           fc := #mb.fc.read_input_reg,  // Function code.
           d_addr := 5017,               // Data address.
           d_len := 2,                   // Data length.
           data := #flow,                
           mb := #mb);                   // Same udt as on the controller.

"mb_query"(unit := #unit,
           fc := #mb.fc.read_input_reg,  
           d_addr := 5025,
           d_len := 2,
           data := #pressure,            // The result will be stored 		   
           mb := #mb);                   // inside the connected variable.

"mb_device_footer"(device := #device_udt, mb := #mb);
// -----------------------------------------------------------------------



// -----------------------------------------------------------------------
// Device block for: Siemens - PAC3200

"mb_device_header"(device := #device_udt, mb := #mb);

"mb_query"(unit := #unit,                 // #unit will be input on the device block. 
           fc := #mb.fc.read_holding_reg, // 3 .
           d_addr := 13,                  // mb offset. Start read at address 13.
           d_len := #mb.c.auto_len,       // Length is calculated based on the size of "data".
           data := #current,		      // #current is a array of 3 reals.
           mb := #mb);                    // #mb will be input on the device block.

"mb_query"(unit := #unit,
           fc := #mb.fc.read_holding_reg,
           d_addr := 55,
           d_len := #mb.c.auto_len,
           data := #common,
           mb := #mb);

"mb_device_footer"(device := #device_udt, mb := #mb);
// -----------------------------------------------------------------------
```
   
Requirements:
 - TIA-portal: v13, sp1, upd8 (or greater)
 - S7-1200: firmware version >= 4.1.3
 - S7-1500: not tested, but should work fine.
 - S7-300 and S7-400: Not supported.

```
The software is not affiliated with Siemens AG
```  