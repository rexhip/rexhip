Modbus API For Siemens S7 PLC's.
---------------------------------------------

```
Author:   Ola Bjørnli
License:  MIT-license
Web:      https://github.com/olab84/TrexHippo
```

The library extend on MB_MASTER and MB_CLIENT, the modbus blocks that comes along with TIA-portal. The library is not an attempt to reinvent the wheel, by doing what those blocks already do. Rather it's an attempt to expand the functionality of the existing blocks, and to create a common API for modbus devices.

Key features:
 - Makes it easy to split the program in to reusable interface blocks.
 - Interface blocks can easily be reused and combind in new programs.
 - A clean API, which helps to cut engineering time.
 - Reduce idle time, by skipping queries that has led to recurring timeouts before. Retries will be done ocatonally.
 - The library select queries from the interface blocks in turn, this prevent one interface block from occupying the bus for long periods of time.
 - Logging features for development and debugging.

```pascal
// =========================================================
// A modbus RTU example that illustrate the library. 
// Support for modbus tcp is also included.

#mb_master_ctrl(
    hardware_id := "Local~CB_1241_(RS485)", 
    baud := 9600, // bps
    parity := true, // Enable even parity.
    timeout := T#500ms,       
    mb := #mb ); // A udt that comes along.

// Instances of device blocks for ABB Aqua master. (interface blocks)
// (unit = station address)
#abb_aquaMaster_3_instance_1(unit := 1, mb := #mb); 
#abb_aquaMaster_3_instance_2(unit := 2, mb := #mb);

// Instances of device blocks for Siemens PAC3200. 
#siemens_PAC3200_instance_1(unit := 3, mb := #mb);
#siemens_PAC3200_instance_2(unit := 4, mb := #mb);
#siemens_PAC3200_instance_3(unit := 5, mb := #mb);
// =========================================================
```


```pascal
// ====================================================================================
// Device block for: ABB - AquaMaster 3 - Electromagnetic flow meter

"mb_device_header"(device := #device_udt, mb := #mb);

// If modicon convention addressing is prefered, then use #mb.c.fc.modicon.read for 
// the fc-parameter. The function code will then be determine by the address range 
// eg. 40001 corresponds to the first holding register.

"mb_query"(unit := #unit,                  // Station address.
           fc := #mb.c.fc.read.input_reg,  // Function code.
           d_addr := 5017,                 // Data address.
           d_len := 2,                     // Data length.
           data := #flow,                
           mb := #mb);      // Same udt as on the controller.

// The result will be stored in the connected variable of data. The variable can 
// be any datatypes, including arrays and udt's.         

"mb_device_footer"(device := #device_udt, mb := #mb);
// ====================================================================================
```


```pascal
// ====================================================================================
// Device block for: Siemens - PAC3200

"mb_device_header"(device := #device_udt, mb := #mb);

"mb_query"(unit := #unit,                   // - #unit is a input variable.
           fc := #mb.c.fc.read.holding_reg, // - Function code 3.
           d_addr := 13,                    // - Start read at address 13.
           d_len := #mb.c.auto_len,         // - Length is calculated automatically 
           data := #current,                //   based on the size of "data". 
           mb := #mb);                      // - #mb is a inOut variable.
                                          
"mb_query"(unit := #unit,                 
           fc := #mb.c.fc.read.holding_reg, 
           d_addr := 55,                  
           d_len := #mb.c.auto_len,       
           data := #frequency,
           mb := #mb);

"mb_device_footer"(device := #device_udt, mb := #mb);
// The #device_udt contains a log, flags, configuration and internal states.
// Implementing the device header and the footer give many benefits, but isn't
// required.
// ====================================================================================
```
   
Requirements:
 - TIA-portal: v13, sp1, upd8 (or later)
 - S7-1200 or S7-1500. (S7-1200 firmware version >= 4.1.3)

Quick starter quide:
 - Download the latest relase. (https://github.com/olab84/TrexHippo/releases)
 - Start a new prodject in TIA-portal, and then add new PLC.
 - Localise "External Source files" in the tree structure. Inside the downloaded zip file, the following files should be imported: 
   mb_lib.scl, mb_lib.udt and mb_start_examples.scl
 - Compile once more to get rid of all the errors.
 - Continue read the "README" FC and study the start example.

```
The software is not affiliated with Siemens AG.
```  
