Rexhip - Improved modbus API for Siemens PLC's.
---------------------------------------------
Author:   Ola Bjørnli

Key features:
 - Makes it easy to create and split a program in to reusable «device blocks» (interface blocks).
 - Device blocks can easily be reused and combined in new programs.
 - A clean API, which helps to cut engineering time.
 - Reduce idle time, by skipping queries that has led to recurring timeout before. Retries will be done occasionally.
 - Logging features for development and debugging.
 - The library extend on MB_MASTER and MB_CLIENT, the modbus blocks that comes along with TIA-portal.
 - Free under the MIT-license.

```pascal
// A complete modbus RTU example that illustrate the library. 
// Support for modbus TCP is also included.

"mb_master_ctrl"(hardware_id := "Local~CB_1241_(RS485)", 
                 baud := 9600, // bps
                 timeout := T#500ms,       
                 mb := #mb ); // A udt that comes along.

// Instances of device blocks for Siemens PAC3200. 
"siemens_PAC3200_DB1"(unit := 1, mb := #mb);
"siemens_PAC3200_DB2"(unit := 2, mb := #mb);
```


```pascal
// Device block for: Siemens - PAC3200

"mb_query"(unit := #unit,                // Station address.
           fc := #mb.c.read.holding_reg, // Function code 3.
           d_addr := 13,                 // Read address 13.
           d_len := 1,                   // Data length.
           data := #resault_data_1,      //   
           mb := #mb);                   // Same udt as above.

// The result will be stored in the connected variable of data. 
// The variable can be any data types, including arrays and udt's

"mb_query"(unit := #unit,                 
           fc := #mb.c.read.holding_reg, 
           d_addr := 55,                  
           d_len := #mb.c.auto_len,       
           data := #resault_data_2,             
           mb := #mb);

// The library will take care of executing the queries, one by 
// one. This is achieved by two counters inside the "mb-udt", 
// one that is increased for each call of mb_query, and one 
// other that is increased each time a query finishes. However 
// this is all taken care of behined the scenes. 
```
   
Requirements:
 - Software: TIA-portal: v13, sp1, upd8 (or later)
 - Hardware: S7-1200 or S7-1500. (S7-1200 firmware version >= 4.1.3)

Quick starter guide:
 - Download the latest release. (https://github.com/olab84/rexhip/releases)
 - Start a new project in TIA-portal, and then add new PLC.
 - Localise "External Source files" in the tree structure. Inside the downloaded zip file, the following files should be imported: 
   mb_lib.scl, mb_lib.udt and mb_start_examples.scl
 - Select all the imported files, right click them and choose "Generate blocks from source".
 - Compile once more to get rid of all the errors.
 - Continue read the generated "README" FC, and study the start examples.

```
The software is not affiliated with Siemens AG.
```  
