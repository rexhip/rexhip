### Station blocks (SB)

The library introduce a concept called station blocks (SB). A SB correspond to GSD-file for profibus, it's a device profiles for one specific modbus device, containing all the queries needed to communicate with that specific modbus device. Setup modbus communication with a VFD (Variable-frequency drive) for example, can take a work day or two. The idea is that, it can be done once and the SB’s can be shared and reused in new applications. Different SB's can easily be combined in the same application, and there can be muliple instances of each SB. The library includes many predefined SB’s, that is freely available, new contributions to the repository are welcome. 

A SB can plug into both modbus tcp and modbus rtu application, this is quite convenient if a tcp-rtu-gateway is used.

```pascal
// Every SB should starts with a station header. #sb bellow, is a special 
// udt that comes along with the library. (mb_station_block_udt)
"mb_station_block_header"(sb := #sb, mb_query := #mb_query);

// #mb_query should be inOut-parameter on the block.

// Device address is the same for all queries, and therefore only need to 
// be defined once. #mb_addr is typically a input parameter on the block.
#mb_query.mb_addr := #mb_addr;

// Queries for each function codes are usally grouped together and the 
// function code is defined once above the queries.
#mb_query.mode := #mb_query.c.read.holding_reg,
#mb_query(data_addr := 123, data_ptr := #resault_data_query_1);
#mb_query(data_addr := 456, data_ptr := #resault_data_query_2);
#mb_query(data_addr := 789, data_ptr := #resault_data_query_3);

// Another group of queries with a different function code.
#mb_query.mode := #mb_query.c.read.input_reg,
#mb_query(data_addr := 123, data_ptr := #resault_data_query_4);
#mb_query(data_addr := 456, data_ptr := #resault_data_query_5);

// Each variable connected to data_ptr, is usally a struct, 
// coresponding to data inside the device.

// In the buttom of each SB, after all the quries, the footer should
// be executed. 
"mb_station_block_footer"(sb := #sb, mb_query := #mb_query);

// IMPORTANT: No code that interupt the execution (eg. return)
// should be placed between the header and the foother.

// For this example values are set to zero if communication problems occurs.
IF #sb.out.error_comm THEN
    #resault_data_query_1 := 0;   
END_IF;
```

#### Features of mb_station_block_header and mb_station_block_footer

- sb.out.error: Set true for all errors including including .error_comm
- sb.out.error_comm: Set true after repeating queries resualting in communcation problems. (timeouts or bad crc)
- sb.out.finnish: Set true for one scan, when the query execution is handed over to the next SB.
 
- sb.log.connected_time: The time the device was connected. 01-01-1970 will be showen, if the device has always been connected.
- sb.log.disconnected_time: Last time the device was disconnected.
- sb.log.done_cnt: Count nunmber of successfully queries.
- sb.log.error_comm_cnt: Only communication errors, timeouts or bad crc.
- sb.log.error_exception: All other errors except communication errors.
- sb.log.error_status: status code if there is a query with an error.
- sb.log.error_data_addr: data_addr of the query that has led to error.

- sb.conf.disable: If set ture, all queries will be skipped and query execution is send to the next SB.
- sb.conf.read_only: Only read queries will be executed. If a write query is inserted, it will later be reject at the footer, and the query execution is sent to the next SB. The internal SB counter will be increaded by one.
- sb.conf.max_comm_error: Max number of repeating communication error before the communcation error flag is set. If the flag is set then all the queries inside the SB are skipped, and retries is only done occasionally.
- sb.conf.exec_x_queries: Number of queries inside the station blocks that should be executed at each loop.
- sb.z... Variables for internal use.

The header and the foother will also prevent the offset problem by setting if-statements around queries, the "hiccup" effect.

#### Save memory

The header and foother gives many nice features, though they are not required for the quries to execute. If memory is limited they can be removed. Also then remove #sb-udt in the satic variable section. 
