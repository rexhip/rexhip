### Changelog:

#### v3.7.4 (nov 2023, tia.14) 
- Removed "Optimized block access" from mb_internal_ser. Some users has reported compilation errors.

#### v3.7.0 (Jul 2023, tia.14) 
- Fixed a bug in mb_read_buffer at line 7, 
  deser_err := "mb_internal_ser"(action := 3 // prior 1.
  Users affected by this bug would allready have notised, since data will not be 
  recived when mb_read_buffer was used. The bug was introduced in v3.5.0. 
  Thank you very much to the user who reported this bug.
- Better description on how to change serial settings.

#### v3.6.0 (okt 2021, tia.14) 
- Fixed a bug regarding modbus tcp, the bug was introduced with  a new feature in 
  v3.3.0. mb_tcp_ctrl, line 77, #mb_query.z.q.data_addr was assigned to MB_DATA_ADDR 
  The bug affect modbus tcp data_addr offset. Eg when mb_query.c.read.holding_reg
  was used, address 40001 equal to offset of zero, after this fix address zero is 
  offset zero. 

#### v3.5.0 (Jul 2021, tia.14) 
- Moved Serialize and Deserialize into the fc mb_interal_ser. This is a 
  workaround regarding some users repporting compilling error about access to
  optimized memory in mb_query.
- Clean up some comments.
- Removed old versions, download was all to huge 31MB.

#### v3.4.2 (Jun 2021, tia.16)
- Recompile all blocks again with TIA-v16. This version is also fully 
  compatible with TIA-portal v17. No changes had been done to the code.
- In the pevious version v3.4.1, some blocks had several versions of the same 
  type, for this reason some programs will not compile.

#### v3.4.1 (Jan 2021)
- Recompile all blocks with TIA-v16

#### v3.4.0 (Sep 2020, tia.14)
- Bug fix of new feature introduced in v3.3.0, where one client can connect to 
  multiple servers. The bug affect the blocks mb_query_range, mb_query_bits and 
  mb_execute. It doesn't affect use of rtu or regular tcp. Code snippet added in 
  mentioned blocks: mb_query.z.run.state <> EXEC_QUERY.
- Change to mb_watchdog for avoiding compiling warning.
- Reorganization start examples folders.
- Change the name master to leader
- Replaced termology master and slave with more inclusiv language, they are now 
  named leader and follower. This is in line with what the big tec companies 
  allready have done. The controller blocks are also renamed, new names are 
  mb_rtu1200_ctrl, mb_rtu1500_ctrl and mb_tcp_ctrl

#### v3.3.0 (May 2020)
- Change ctrl to use mode 0, 1 and 2, so error code 8188 does't appear, this may
  be a issue on plc's with older firmware.
- rtu automatic timeout caluction is changed and simplifed.

#### v3.2.0 (Apr 2020)
- Muliple tcp-connections for one mb_client.
- mb_client_ctrl, refoctoring code to fit the new muliple-tcp-connection api.
- Query-range api, including mb_query_range, mb_read_buffer, mb_buffer_get, 
  mb_swap_word and mb_little_endian.
- mb_master_1200_ctrl, default timeout gain is increased from 2 to 3.
- Improvment, mb_station_block_foother, bottom ORIGIN or instead of INSERT_QUERY.
- Improvment, mb_client_ctrl. #connected_least_once set true after mb_client.
- Fixed minor bug in mb_sequence_init introduced in v3.1.0, mode need to be set 
  after the if-statement.
- IP-addr, array of usint insted of bytes. This makes it easier to read ip when 
  monitoring plc online.
- Better comments of the code in mb_sequence.
- [.z.sb.set_err] A variable for set all error flags on all sb's true.
- [.z.sb.exec_all] Make all queries be execute right away, without switching
  execution between different sb's.
- Forwarding any error from sb to error on ctrl. (#mb_query.z.sb.err)
- For mb_client_ctrl timeout limited to max 10s
- Interface udt's.
- Fast error detection on disconnect (mb_client_ctrl bottom mb_query.z.sb.set_err).
- Condition for changing query-state: state <> EXEC_QUERY. mb_query, 
  mb_station_block_header and mb_tcp_connection_foother. This is need for muliple
  connection feature.
- sb.conf.unit, transfered to mb_addr in mb_station_block_header.

#### v3.1.0 (17 Oct 2019)
- Fixed bug regarding read-only feature. When flag was set, the execution will 
  halt inside one sb, when a write-query is inserted.
- Added some more start examples.
- SB's are seperated in to two folders, tested and untested.
- Start tracking changes in sb's. Changelog_sb.md.
- Renamed #sb.out.error_comm to #sb.out.communication_error
- New sequence (state machine) interface, for low priority queries.
- sid halt api. Makes it possible to stop sid from increment.

#### v3.0.0 (11 Apr 2019)
- New halt api, for slowing down execution for modbus tcp.
- Replaced insert and insert2 with a state variable.
- Rewrite of all three ctrl blocks for new state var.
- Rewrite of mb_delay and mb_delay_between_queries.
- Changes in mb_query_bits.
- Updated some sb-blocks
- SB skip_code feature.
- Improved timeout calculation for S7-1200 rtu.
- New fc mb_timeout_rtu_calc.
- Improved comments.
- Removed feature "de-/serialize error" introduced in 2.5.0, it's isn't need.
- Rewrite and simplify mb_client_ctrl, no-connection will not trigg a disconnect.
- Qid zero will not set req false, on client and master.
- Change timeout variables on rtu ctrl.

#### v2.5.0 (17 Feb 2019)
- Moved from scl-files to Siemens library format. (v14)
- Renamed some internal varsiables, like «sid»
- Improved comments.
- Make de-/serialize error affect the common error falg on the sb-var. 
- New Station blocks
- Station blocks, clean up.
- OPC-UA checkboxes.

#### v2.4.0 (25 Aug 2018)
- Added the function block mb_delay_between_queries
- modbus rtu: Parity error (80E1) and Framing error (80E2) included in the expression for comm.error.
- Added mb_delay_between_queries, replaces mb_delay.
- mb_query_bits and mb_delay moved to extended features.
- Added mb_execute and mb_dataptr_eq_buffer to extended features.

#### v2.3.4 (22 Mar 2018)
- Bug fix in mb_delay.
- swap_real is removed from library.
- Updates to documentation.
- New SB's

#### v2.3.3 (20 Feb 2018)
- mb_delay is now part of the library. The function is included in tcp example.
- For modbus tcp, setting qid to zero will not disconnect.
- New station blocks
- Documentation improvments.

#### v2.3.2 (5 Jan 2018)
- Refactoring mb_query_bits, and fixed a bug.
- Added mb_delay function inside extend pack.
