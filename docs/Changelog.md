### Changelog:

#### 3.0.0
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
- Qid zero will not set req false, on cleint and master.
- Change timeout variables on rtu ctrl.


#### 2.5.0
- Moved from scl-files to Siemens library format. (v14)
- Renamed some internal varsiables, like «sid»
- Improved comments.
- Make de-/serialize error affect the common error falg on the sb-var. 
- New Station blocks
- Station blocks, clean up.
- OPC-UA checkboxes.

#### 2.4.0
- Added the function block mb_delay_between_queries
- modbus rtu: Parity error (80E1) and Framing error (80E2) included in the expression for comm.error.
- Added mb_delay_between_queries, replaces mb_delay.
- mb_query_bits and mb_delay moved to extended features.
- Added mb_execute and mb_dataptr_eq_buffer to extended features.

#### 2.3.4
- Bug fix in mb_delay.
- swap_real is removed from library.
- Updates to documentation.
- New SB's

#### 2.3.3
- mb_delay is now part of the library. The function is included in tcp example.
- For modbus tcp, setting qid to zero will not disconnect.
- New station blocks
- Documentation improvments.

#### 2.3.2
- Refactoring mb_query_bits, and fixed a bug.
- Added mb_delay function inside extend pack.
