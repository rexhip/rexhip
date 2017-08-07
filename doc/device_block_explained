```pascal
// Start example for a device blocks. A device block is a FB  that is
// written for one specific modbus device.


// Every device block should start with a device header. Though it
// isn't required.
"mb_device_header"(common := #common, mb := #mb);


// First query example
"mb_query"(unit := #unit,
           fc := #mb.c.read.holding_reg,
           d_addr := 123,
           d_len := #mb.c.auto_len,
           data := #resault_data_query_1,
           mb := #mb);
//
// A standard modbus telegram
// .------.------.------------.------------.--  ..  ..  -- --.------------.
// | unit |  fc  |   d_addr   |   d_len    |      data       |    CRC     |
// '------'------'------------'------------'-- --  ..  ..  --'------------'
//
// --- unit:
// Device address. 1-247 (RTU station address)
//
// --- fc:
// Modbus function code, supported codes: 1, 2, 3, 4, 5, 6, 15 and 16. Start
// typing "#mb.c." and the auto complete list will show all available function
// codes. 
//
// --- d_addr:
// Data addr, the actual value that will be sent in the modbus telegram.
// Eg. to read holding address 123, you simply pass 123 to d_addr and
// "#mb.c.read.holding_reg" (3) to the fc-parameter. 40001 should NOT be
// added to 123.
//
// --- d_len:
// Data length. By passing zero (#mb.c.auto_len) to the parameter the
// library will calculate this parameter automatically. In the example above
// "data" consist of two words, so the value of d_len inside the telegram
// will also be two. By entering d_len manually the library will run a bit 
// faster.
//
// --- data:
// Container for data that will be send or receive. The parameter is not
// limited to words, but can contain any data types, including: real,
// bytes, arrays and udt's
// Though, two criterion most to be followed:
// 1. Only whole registers. (Bytes and bools should add up to 16 bits)
// 2. The modbus protocol limit each query to a maximum of 123 words.
//    (Sometimes up to 125 words)
//
// --- mb:
// The udt that bind everything together. 


// Similar query as above, except two input register are read. Any number
// of queries can be added, the library will take care of executing them,
// one by one.
"mb_query"(unit := #unit,
           fc := #mb.c.read.input_reg,
           d_addr := 1234,
           d_len := 2,
           data := #data_query_2,
           mb := #mb);


// Modicon convention addressing:
"mb_query"(unit := #unit,
           fc := #mb.c.mode.read,
           d_addr := 40005,
           d_len := #mb.c.auto_len,
           data := #data_query_3,
           mb := #mb);
// The parameters: unit, d_len, data and mb, work the same way as in the
// previous example. To use the Modicon convention, one of the fc-constants
// bellow should be used:
//   - #mb.c.mode.read           -> mb function code: 1, 2, 3 and 4  
//   - #mb.c.mode.write          -> mb function code: 15 and 16      
//   - #mb.c.mode.write_single   -> mb function code: 5 and 6        
// 
// When the modicon convention is used, the function code is "embedded" in
// to d_addr. Eg. query 40005 will actually query holding register with
// data address (offset) 4. Keep in mind that modes for mb_master and
// mb_cleint are shifted, e.g. 200 corresponds to mode 0.


// A write query executed with function code "6" (write.single_holding_reg)
"mb_query"(unit := #unit,
           fc := #mb.c.write.single_holding_reg,
           d_addr := 42,
           d_len := 1,
           data := #data_query_4,
           mb := #mb);
// Some (old) modbus devices doesn't support modbus function code "16"
// "write.holding_reg". In that case function code number "6" need to
// be used ("mb.c.write.single_holding_reg"). 


// Header and footer
// -----------------------------------
// As mention at the top the mb_device_header isn't required However if
// the "footer" is implemented then the "header" is also nedded, else the
// library will not work. No query should go before the "header" or after
// the "footer".
"mb_device_footer"(common := #common, mb := #mb);
// Benefits of the header and the fotter :
//  - Logging capacities: Inside the device-udt there is logging of
//    successfully and failed queries, which is helpful
//    for debugging. See: "#common.log. ..."
//  - "#common.out.error" a common error flag that is set if any of the
//    intermediate queries between mb_device_footer and mb_device_header
//    gives an error.
//  - "#common.out.communication_error" a error flag that will be set after
//    number of repeating timeout of the intermediate queries. Intended
//    to reset values when communication problems occur. The number of
//    repeating timeout before the flag is set can be configured with
//    "#common.conf.max_repeating_timeouts".
//  - Only one query for each device is allowed to be executed for
//    every loop. This is to avoid devices with many queries to occupy
//    the bus for long periods of time.
//  - Prevent the impact of setting if-condition around queries. The
//    "hiccup" effect mentioned above.


// For this example values are set to zero if communication problems accrue.
IF #common.out.communication_error THEN
    #resault_data_query_1 := 0;
    
    #data_query_2[1] := 0;
    #data_query_2[2] := 0;
END_IF;
```
