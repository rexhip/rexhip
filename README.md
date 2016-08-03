Lightweight Modbus Abstraction Layer Library.
---------------------------------------------
For Siemens S7-1200 and S7-1500 PLC's.

```
 
Author:   Ola Bjørnli
Version:  0.2_beta10
License:  GPLv2, MIT (pick the one of your need)
Web:      http://mb.sn7.no
          http://github.com/olab84/sn7mb

```

All though the new plc series from Siemens has built in support for modbus. It's required to build some additional logic to make the queries being executed in order. This software address that issue, the example bellow illustrate how easy modbus can be done with this library:

```

// A modbus RTU example shown bellow, the library also 
// support modbus tcp.

#mb_rtu(hardware_id := "Local~CB_1241_(RS485)",
        baud := 9600,
        parity := false,
        timeout := T#300ms,
        buffer_db_any := "buffer",
        buffer_variant := "buffer",
        mb := #mb);

// Query 1 - Read holding register.
"mb_read"(unit := 5,     // device address
          d_addr := 34,   // data address, 
          data := #resualt_data,  
          mb := #mb); // same udt as on the block above.
		  
// "data" is a inOut variant parameter where the query result 
// will be stored. The parameter can be any kind of data type, 
// including arrays and udt's. The datatype should match 
// the datatype of the registers being queried.

// The function will automatically calculate the length field
// in the modbus telegram. Eg. if "data" is an array of 4 
// dwords, then the length will automatically be set to 8.

// "d_addr" is the raw telegram address, there is no adding 
// 40001, or no senseless waste of costly engineers hours 
// wasted of figure out a offset. Just type the address from
// the data sheets. (Same as for JBus)

// Query 2 
"mb_read"(unit := 9,
          d_addr := 25,
          data := #resualt_data_2,
          mb := #mb);	
		  
```
		  
Just by adding more "mb_read" function, more queries can 
be included. The library will take care of executing the 
queries one by one in order. There is a corresponding 
function mb_write. For coils and inputs there is also
additional functions. 

If a timeout occur, the library is smart enough to skip other
quires with the same device address, until all other queries
has been executed. Other functionality worth mention, is the
error log, which is great for debugging.

For S7-1200: firmware version >= 4.1.3
	 
Download the blocks and the example from github to get started.
I you find scl-programming hard, you can of course also use
lad or fbd.
