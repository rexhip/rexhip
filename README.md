Modbus API For Siemens S7 PLC's.
---------------------------------------------

```
Author:   Ola Bjørnli
License:  MIT-license
Web:      http://github.com/olab84/sn7mb
```

The library extend on MB_MASTER and MB_CLIENT, the modbus blocks that comes along with TIA-portal. The library is not an attempt to reinvent the wheel, by doing what those blocks already do. Rather it's an attempt to expand the functionality of the existing blocks, and to create a common clean API for "device blocks" (interface blocks).

Key features:
 - Eliminate global states, which make it possible to create reusable device blocks. 
 - Clean and readable API, this makes it possible to create large scale application, and it helps to cut engineering time.
 - Advanced timeout handler that reduce idle time, and sophisticated bus sharing mechanism.
 - Logging features for development and debugging.
 - Results can be stored inside optimized memory areas.

```pascal
// A modbus RTU example that illustrate the library. 
// (Support for modbus tcp is also included).

#mb_master_controller(
    hardware_id := "Local~CB_1241_(RS485)", //  
    baud := 9600,                           // bps
    parity := true,                         // Enable even parity.
    timeout := T#500ms,   
    buffer_db_any := "modbus_rtu_buffer",   // - A global DB where optimized is off,
    buffer_variant := "modbus_rtu_buffer",  //   should contain a array of 125 words
    mb := #mb );                            // - A udt that comes along 

// Instances of device blocks for ABB Aqua master 3	
#abb_aquaMaster_3_instance_1(unit := 1, mb := #mb);
#abb_aquaMaster_3_instance_2(unit := 2, mb := #mb);

// Instances of device blocks for Siemens PAC3200 
#siemens_PAC3200_instance_1(unit := 3, mb := #mb);
#siemens_PAC3200_instance_2(unit := 4, mb := #mb);
#siemens_PAC3200_instance_3(unit := 5, mb := #mb);



// -----------------------------------------------------------------------
// Device block for: ABB - AquaMaster 3 - Electromagnetic flow meter

// A customized device block need to be created for all device, once
// it's created it con be placed inside a global library and be reused.
// The pattern bellow should be intuitive, the library will take care
// of executing the queries one by one.

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
           data := #pressure,       // - The result will be stored 		   
           mb := #mb);              //   inside the connected variable.
		                            //   Can be a array or a udt. 
"mb_device_footer"(device := #device_udt, mb := #mb);

// The #device_udt contains a log, flags, configuration and internal states.
// Implementing the device header and the footer give many benefits, but isn't
// required.
// -----------------------------------------------------------------------



// -----------------------------------------------------------------------
// Device block for: Siemens - PAC3200

"mb_device_header"(device := #device_udt, mb := #mb);

"mb_query"(unit := #unit,                 // #unit will be a input on this device block. 
           fc := #mb.fc.read_holding_reg, // (3)
           d_addr := 13,                  // mb offset. Start read at address 13.
           d_len := #mb.c.auto_len,       // Length is calculated based on the size (bytes) of "data".
           data := #current,		      // #current is a array of 3 reals. (See data sheet of device)
           mb := #mb);                    // #mb will be inOut on this device block.
                                          
"mb_query"(unit := #unit,                 
           fc := #mb.fc.read_holding_reg, 
           d_addr := 55,                  
           d_len := #mb.c.auto_len,       
           data := #common,               // A udt with common data. (See data sheet of device)
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
