Lightweight Modbus Abstraction Layer Library.
For Siemens S7-1200 and S7-1500 PLC's.

Author:   Ola Bjørnli
Version:  0.2_beta1
License:  GPLv2, MIT (pick the one of your need)
Web:      http://mb.sn7.no
          http://github.com/olab84/sn7mb

The example bellow illustrate have easy modbus can be done
with this software:

--------------------------------------------------------------

```
// RTU example show bellow, the library also include 
// function blocks for modbus tcp.

#mb_rtu(hardware_id := "Local~CB_1241_(RS485)",
        baud := 9600,
        parity := false,
        timeout := T#3000ms,
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
--------------------------------------------------------------
		  
Just by adding more "mb_read" function, more queries can 
be included. The library will take care of executing the 
queries one by one in order. There is a corresponding 
function mb_write. For coils and inputs there is also
additional functions. 

If a timeout occur, the library is smart enough to skip other
quires with the same device address, until all other queries
has been executed. Other functionality worth mention, is the
error log, which is great for debugging.
	 
Download the blocks and the example from github to get started.